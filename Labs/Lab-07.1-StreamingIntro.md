<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 7.1: Kafka Streams - intro

---

### Change Log

Updated 2023-10-28

Rod Davison

---

### Overview
Setup a Kafka streaming application

### Depends On

### Run time
20 mins

## Step 1: Run Consumer

On console...

Use kafkacat

```bash
kafkacat -q -C -b localhost:9092 -t clickstream -f 'Partition %t[%p], offset: %o, key: %k, value: %s\n'
```

or console-consumer

```bash
~/apps/kafka/bin/kafka-console-consumer.sh \
        --bootstrap-server localhost:9092 \
        --property print.key=true --property key.separator=":" \
        --topic clickstream
```

## Step- : Clickstream Producer

File : `src/main/java/x/utils/ClickStreamProducer.java`

We will continue use this producer

Run the producer in Eclipse, Right click on the file and run as 'Java Application' 

Make sure it is sending messages as follows
- key : Domain
- value : clickstream data
- example:

```console
  key=facebook.com, value={"timestamp":1451635200005,"session":"session_251","domain":"facebook.com","cost":91,"user":"user_16","campaign":"campaign_5","ip":"ip_67","action":"clicked"}
```

## Step 3: Streaming Consumer 1

This consumer will read and print a KafkaStream.

File : `src/main/java/x/lab07_streams/StreamsConsumer1.java`

Run the `lab07_streams/StreamsConsumer1` 

## Step 4:  Run `ClickStreamProducer`

Run the `utils.ClickStreamProducer` in Eclipse

Expected output

```console
[[KSTREAM-SOURCE-0000000000]: facebook.com, {"timestamp":1451635200040,"domain":"facebook.com","cost":22,"user":"user_68","campaign":"campaign_5","ip":"1.3.2.5","action":"blocked"}
[KSTREAM-SOURCE-0000000000]: facebook.com, {"timestamp":1451635200045,"domain":"facebook.com","cost":66,"user":"user_46","campaign":"campaign_4","ip":"3.2.5.1","action":"viewed"}
[KSTREAM-SOURCE-0000000000]: gmail.com, {"timestamp":1451635200050,"domain":"gmail.com","cost":55,"user":"user_1","campaign":"campaign_9","ip":"3.3.4.0","action":"blocked"}
```
---

## End Lab