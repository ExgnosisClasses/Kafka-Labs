<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 7.2: Kafka Streams - Foreach


---

### Change Log

Updated 2023-10-28

Rod Davison

---

## Overview

Setup a Kafka streaming application

## Depends On

## Run time

20 Minutes

## Step 1:  Streaming Consumer 1

This consumer will read and print a KafkaStream.

Open the file `src/main/java/x/lab07_streams/StreamsConsumer2_Foreach.java`

Run the `lab07_streams/StreamsConsumer2_Foreach`

## Step 2: Run `ClickstreamProducer`

Run the `utils.ClickStreamProducer` in Eclipse

Expected output

```console

[kstreams starting on clickstream
FOREACH [1]:: KEY:gmail.com, VALUE:{"timestamp":1451635200005,"domain":"gmail.com","cost":12,"user":"user_18","campaign":"campaign_3","ip":"2.3.3.0","action":"clicked"}
FOREACH [2]:: KEY:gmail.com, VALUE:{"timestamp":1451635200010,"domain":"gmail.com","cost":26,"user":"user_83","campaign":"campaign_1","ip":"1.1.5.8","action":"blocked"}
```

Shut down the consumer

---

## End Lab