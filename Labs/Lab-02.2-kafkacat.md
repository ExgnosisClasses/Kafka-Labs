<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 2.2: Kafkacat
--

### Change Log

Updated 2023-10-28

Rod Davison

---

## Overview

[kafkacat](https://github.com/edenhill/kcat) is really useful tool to deal with Kafka.  In this lab, we will setup Kafkacat and use it

## Run time

15 minutes

## Step 1: Install `kafkacat`

Install kafkacat on your VM

```bash
sudo apt update

sudo apt install -y kafkacat
```

## Step 2: Get Kafka Cluster Info

```bash
kafkacat -L   -b localhost:9092
```

## Step 3: Producer / Consumer mode

In a terminal. start Kafkacat in producer mode for the `test` topic

```bash
kafkacat -P -b localhost:9092   -t test
```

In a second terminal, start kafkacat in consumer mode

```bash
# wait for new messages
kafkacat -C -b localhost:9092   -t test
```

Type some messages in the producer terminal and observe the output in consumer terminal

## Step 4: More Formatting Options

Close the kafkacat consumer by hitting Ctrl+C in the consumer terminal and try the following:

```bash
kafkacat -q -C -b localhost:9092 -t test -f 'Partition %t[%p], offset: %o, key: %k, value: %s\n'
```

## Step 5: More Options for Producing

The default is to produce messages by reading from STDIN and writing to the topic `test`

```bash
kafkacat -P -b localhost:9092   -t test
```

Or you can pipe a file into a topic. Create some dummy input by creating a text file with a number of lines of text in Visual Studio Code. Make sure you save the file into the same directory  you will be running the `kafkacat` from. 

```bash
cat test.txt   |  kafkacat -P  -b localhost:9092  -t test
```

Producing messages with key-values

```bash
kafkacat -P -b localhost:9092 -t test -K :
# Then type
#    k1:v1
#    k2:v2
```

Produce messages from a file.  Say our file `data.txt` has data in this format:

```text
k1:v1x
k2:v2x
k3:v3x
```

Use a batch send like this:

```bash
kafkacat -P -b localhost:9092 -t test -K: -l data.txt
```

## Step 6: More Options for Consuming

```bash
# quiet mode
kafkacat -q -C -b localhost:9092   -t test

# wait for new messages
kafkacat -C -b localhost:9092   -t test

# exit after reading all messages
kafkacat -C -b localhost:9092   -t test  -e

# only read last 10 messages and exit
kafkacat -C -b localhost:9092   -t test  -o -10 -e
```

#### More formatting options

Print the key and value
```bash
kafkacat -C -b localhost:9092 -t test -f 'key: %k, value: %s \n'
```

More detailed output 
```bash 
kafkacat -C -b localhost:9092 -t test -f 'Topic %t[%p], offset: %o, key: %k, value: %s, (length: %S bytes) \n'
```
Print timestamp of messages (%T)
```bash
 kafkacat -q -C -b localhost:9092 -t test -f 'Partition %t[%p], offset: %o, timestamp: %T,  key: %k, value: %s\n'
```
More usage details [see Kafkacat page](https://github.com/edenhill/kcat)

## References

* [Using Kafkacat to troubleshoot Kafka](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/KafkaIntegrationGuide/TroubleShooting/UsingKafkacatToTroubleShootIssues.htm)
* [Learn how to use Kafkacat](https://dev.to/de_maric/learn-how-to-use-kafkacat-the-most-versatile-kafka-cli-client-1kb4)

---

## End Lab