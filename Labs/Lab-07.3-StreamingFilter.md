<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 7.3: Kafka Streams - Filter

---

### Change Log

Updated 2023-10-28

Rod Davison

---

## Overview

Filter a Kafka stream

## Depends On

[7.1 streaming intro](07.1-streaming-intro.md)

## Run time

20 Minutes


## Step 1:  Streaming Consumer 2

This consumer will read a KafkaStream and extract only `action=clicked` events.

Open the file  `src/main/java/x/lab07_streams/StreamsConsumer3_Filter.java`

Run the `lab07_streams/StreamsConsumer3_Filter` in Eclipse

## Step 2: Run

Run the `lab07_streams/StreamsConsumer3_Filter` in Eclipse

Run the `utils.ClickStreamProducer` in Eclipse

Expected output below.

Notice `KStream-filtered-CLICKED` will only have 'action=clicked' events.

```console
kstreams starting on clickstream
[KSTREAM-FILTER-0000000001]: twitter.com, {"timestamp":1451635200010,"domain":"twitter.com","cost":14,"user":"user_38","campaign":"campaign_4","ip":"1.3.3.9","action":"clicked"}
[KSTREAM-FILTER-0000000001]: facebook.com, {"timestamp":1451635200015,"domain":"facebook.com","cost":50,"user":"user_39","campaign":"campaign_6","ip":"1.2.8.3","action":"clicked"}
[KSTREAM-FILTER-0000000001]: twitter.com, {"timestamp":1451635200035,"domain":"twitter.com","cost":11,"user":"user_79","campaign":"campaign_1","ip":"1.3.3.6","action":"clicked"}
[KSTREAM-FILTER-0000000001]: gmail.com, {"timestamp":1451635200020,"domain":"gmail.com","cost":59,"user":"user_5","campaign":"campaign_3","ip":"1.1.2.0","action":"clicked"}
[KSTREAM-FILTER-0000000001]: gmail.com, {"timestamp":1451635200045,"domain":"gmail.com","cost":78,"user":"user_17","campaign":"campaign_2","ip":"1.2.6.0","action":"clicked"}
[KSTREAM-FILTER-0000000001]: facebook.com, {"timestamp":1451635200015,"domain":"facebook.com","cost":33,"user":"user_78","campaign":"campaign_5","ip":"3.3.2.6","action":"clicked"}
[KSTREAM-FILTER-0000000001]: facebook.com, {"timestamp":1451635200030,"domain":"facebook.com","cost":88,"user":"user_14","campaign":"campaign_4","ip":"2.1.9.1","action":"clicked"}
[KSTREAM-FILTER-0000000001]: facebook.com, {"timestamp":1451635200040,"domain":"facebook.com","cost":25,"user":"user_55","campaign":"campaign_2","ip":"2.2.1.3","action":"clicked"}

```
 Shut down the consumer
 
---

## End Lab
