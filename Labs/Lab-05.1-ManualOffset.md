<link rel='stylesheet' href='../assets/css/main.css'/>

# Lab 5.1: Manual Offset

---

### Change Log

Updated 2023-10-28

Rod Davison

---

## Overview

Seek within partition

## Depends on 

Topic `testc` frome previous labs

## Run time

20 Minutes

## Step 1: Set up a Topic

Set up the topic `offsets` to be used in the lab

```bash
~/apps/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic offsets --partitions 2
```

Create a command line producer and add some data to the topic either with the standard command line producer.

```bash
~/apps/kafka/bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic offsets
```
Or 

```bash
kafkacat -P -b localhost:9092   -t offsets
```
Add some random data:

```console
Alfa
Bravo
Charlie
Delta
Echo
Foxtrot
Golf
Hotel
India
Juliett
Kilo
Lima
Mike
November
Oscar
Papa
Quebec
Romeo
```
## Step 1: Consumer

Open the file `src/main/java/x/lab05_offsets/ManualOffsetConsumer.java` in Eclipse

Make sure the auto commit is disabled.

```java
props.put("enable.auto.commit", "false");
```

Run the consumer in Eclipse
- Right click on file
- Run as 'Java Application'

## Step 2: Inspect the output from Consumer

You will see consumer processing messages.

Pay special attention to OFFSETs.
```console
Received message [18] : ConsumerRecord(topic = offsets, partition = 0, leaderEpoch = 0, offset = 17, CreateTime = 1698595341940, serialized key size = -1, serialized value size = 0, headers = RecordHeaders(headers = [], isReadOnly = false), key = null, value = )
OFFSET : partition:0, offset:18
OFFSET : partition:1, offset:0
```
Stop the consumer program

## Step 3: Rerun the consumer

Rerun the consumer

Note: It may take a few seconds to establish connection to Kafka (because we didn't do a clean shutdown)

Observe the consumer output, you will see the same messages.  Can you explain why?

Stop the consumer

## Step 4: Enable commitSync

Uncomment the following line to enable commitSync

```java
consumer.commitSync();
```

## Step 5: Rerun Consumer

Re-run consumer again and observe what data it is getting 

Stop the consumer and restart the consumer again. 

Observe the data.  What do you see?  Is it still getting 'old data'?

## Step-6: Send Some New Data

Use the console producer to send a couple of new messages

```bash
Earth
Mars
Venus
```

You should see it comes out via consumer.

## Step 7:
 
Shut down all the consumers and producers used at the console and in Eclipse

---

## End Lab

