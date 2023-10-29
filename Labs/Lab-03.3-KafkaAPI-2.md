<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 3.3 : Working With Kafka API

---

### Change Log

Updated 2023-10-28

Rod Davison

---

## Watch and Do

The instructor will walk through the complete lab and explain what is happening at each step. This is your opportunity to clarify any issue you might have about the code or concepts before you try it yourself.


## Run time

40 Minutes

## Step 1 : Create a 'clickstream' topic

Create a new topic for this lab

```bash
~/apps/kafka/bin/kafka-topics.sh  --bootstrap-server localhost:9092  --create  --topic clickstream --replication-factor 1  --partitions 2
```

## Step 2 : Open a console consumer

In a terminal, do either of the following. Use the standard Kafka consumer 
```
~/apps/kafka/bin/kafka-console-consumer.sh \
     --bootstrap-server localhost:9092 \
     --property print.key=true --property key.separator=":" \
        --topic clickstream
```

or use Kafkacat

```bash
kafkacat -q -C -b localhost:9092 -t clickstream -f 'Partition %t[%p], offset: %o, key: %k, value: %s\n'
```

## Step 3 : Run the Producer

In Eclipse, open the file  `src/main/java/x/lab03_api_intro/ClickstreamProducer`.

To run the Producer in Eclipse,
- Right click on 'src/main/java/x/lab03_api_intro/ClickstreamProducer'
- Run as 'Java Application'

In Eclipse console, you should see output something like this:


```console
Sent record [1] (key:youtube.com, value:{"timestamp":1451635200005,"domain":"youtube.com","cost":12,"user":"user_84","campaign":"campaign_7","ip":"3.3.3.0","action":"blocked"}), time took = 258.75 ms
Sent record [2] (key:gmail.com, value:{"timestamp":1451635200010,"domain":"gmail.com","cost":24,"user":"user_11","campaign":"campaign_3","ip":"1.2.8.0","action":"clicked"}), time took = 0.23 ms
Sent record [3] (key:youtube.com, value:{"timestamp":1451635200015,"domain":"youtube.com","cost":14,"user":"user_17","campaign":"campaign_6","ip":"2.1.6.6","action":"clicked"}), time took = 0.19 ms
Sent record [4] (key:gmail.com, value:{"timestamp":1451635200020,"domain":"gmail.com","cost":85,"user":"user_91","campaign":"campaign_2","ip":"1.1.6.2","action":"clicked"}), time took = 0.18 ms
Sent record [5] (key:gmail.com, value:{"timestamp":1451635200025,"domain":"gmail.com","cost":13,"user":"user_61","campaign":"campaign_4","ip":"2.2.7.9","action":"clicked"}), time took = 0.26 ms
Sent record [6] (key:youtube.com, value:{"timestamp":1451635200030,"domain":"youtube.com","cost":23,"user":"user_54","campaign":"campaign_3","ip":"1.1.5.1","action":"clicked"}), time took = 0.18 ms

```

## Step 4 : Monitor Kafka console consumer

Check the messages that have been read by the console consumer.

Are the messages coming in order?  (check the key)  Why or why not?

Can you make the messages come 'out of order'?  

Hint : Reduce the time interval between messages on producer side 

## Step 5: Quick experiment on send modes

The producer is sending records **without** waiting for response

```java
producer.send(record)
```

Take a note at the average time taken to send a record.  Should be around  0.1 - 0.5 ms range.

Now update the code to wait for the response from Kafka broker, as follows

```java
producer.send(record).get()
```

Run the code again, and note the average time to send each record.  How much difference do you notice?

## Step 6 : Run Consumer and Producer from Eclipse
Open the file `src/main/java/x/lab03_api_intro/ClickstreamConsumer.java` in Eclipse

Right click on `src/main/java/x/lab03_api_intro/ClickstreamConsumer.java`

Run as 'Java Application' 

Right click on `src/main/java/x/lab03_api_intro/ClickstreamProducer.java`

Run as 'Java Application'

In Eclipse, monitor output from two of these programs and also monitor what is happening in Kafka console consumer?

## Step 7 : Run multiple consumers

Run `src/main/java/x/lab03_api_intro/ClickstreamConsumer.java`

Again run `src/main/java/x/lab03_api_intro/ClickstreamConsumer.java`

Verify two consumer apps are running in Eclipse

Run `src/main/java/x/lab03_api_intro/ClickstreamProducer.java`

Verify the messages are split between two consumers

Run three consumers and see which ones are getting data.  Can you explain the behavior?

## Step 8: Run the code in terminal

So far, the code has been run from the Eclipse IDE. Now, you will package up the code into `jar` files so they can be run from a terminal

First, in a terminal, change the working directory to be the same directory that the `pom.xml` file is in. In  this case, it is the `Kafka-Lab-Project` but yours may be in a different directory. Use the `ls *xml` command to confirm you are in the right directory

```bash
cd   ~/Kafka-Lab-Project
ls *xml   
``` 

Validate that the `pom.xml` file is valid

```bash
mvn validate
```
There will be several warnings that you can ignore, but you should see something like this

```console 
[INFO] Scanning for projects...
[INFO] 
[INFO] --------------------------< kafka:kafka-labs >--------------------------
[INFO] Building kafka labs 2.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.081 s
[INFO] Finished at: 2023-10-29T04:02:09Z
[INFO] ------------------------------------------------------------------------
``` 
Now build the `jar` file. This will take a while and there may be a number of warnings that won't affect the build.

```bash
 mvn  clean package  -DskipTests
```
The final part of the build should look like this

```console
[INFO] Building jar: /home/ubuntu/Kafka-Lab-Project/target/kafka-labs-2.0-jar-with-dependencies.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  14.073 s
[INFO] Finished at: 2023-10-29T04:05:05Z
[INFO] ------------------------------------------------------------------------
```

Inspect the `target` directory.  You will see 2 jars.

```bash
ls -lh  target/*jar
```

```console
-rw-rw-r-- 1 ubuntu ubuntu 76M Oct 29 04:05 target/kafka-labs-2.0-jar-with-dependencies.jar
-rw-rw-r-- 1 ubuntu ubuntu 77K Oct 29 04:04 target/kafka-labs-2.0.jar
```

`kafka-labs-2.0.jar` only has the classes defined in your code

`kafka-labs-2.0-jar-with-dependencies.jar` has both the classes defined in the code and all dependencies included.  This is a `fat jar` file that allows the application to be run without having to worry about dependencies.

Inspect the classes included in a jar file as follows:

```bash
jar tf target/kafka-labs-2.0.jar   | less
# hit 'q' to exit paging


jar tf target/kafka-labs-2.0-jar-with-dependencies.jar | less
# hit 'q' to exit paging
```

Start the consumer in a new terminal. Ensure that you are in the right directory for you. There will be a lot of errors about `Logger Status` which you can just ignore because they will not affect the lab.

```bash
cd   ~/Kafka-Lab-Project

java -cp target/kafka-labs-2.0-jar-with-dependencies.jar   x.lab03_api_intro.ClickstreamConsumer

# another option is running via maven
mvn exec:java  -Dexec.mainClass=x.lab03_api_intro.ClickstreamConsumer
```
```console
ERROR StatusLogger Unrecognized format specifier [n]
ERROR StatusLogger Unrecognized conversion specifier [n] starting at position 56 in conversion pattern.
Listening on clickstream topic
```
Open another terminal and start the producer/

```bash
cd   ~/Kafka-Lab-Project

java -cp target/kafka-labs-2.0-jar-with-dependencies.jar    x.lab03_api_intro.ClickstreamProducer

# or using maven
mvn exec:java  -Dexec.mainClass=x.lab03_api_intro.ClickstreamProducer
```
The producer will exit as soon as it has generated some messages. Watch the consoles of both producer and consumer

## Step 9: Clean up.

Stop all running producers and consumers either in Eclipse or in terminals

---

## End Lab


