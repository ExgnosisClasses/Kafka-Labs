<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 7.4: Kafka Streaming - Map
---

### Change Log

Updated 2023-10-28

Rod Davison

---

## Overview

Apply `map` transformation for KStreams

## Depends On

07.1-streaming-intro.md

## Run time

20 Minutes

## Step 1 :  Streaming Consumer 3

File : `src/main/java/x/lab07_streams/StreamsConsumer3_Map.java`

This consumer will read a KafkaStream and map the incoming record into key value pair with action.

Example 1:
```
Incoming :
{"timestamp":1451635200005,"session":"session_251","domain":"facebook.com","cost":91,"user":"user_16","campaign":"campaign_5","ip":"ip_67","action":"clicked"}

Output:
("clicked", 1)
```

Example 2:
```
Input :
{"timestamp":1451635200010,"session":"session_224","domain":"foxnews.com","cost":17,"user":"user_89","campaign":"campaign_4","ip":"ip_57","action":"viewed"}

Output:
("viewed", 1)
```

Run the `lab07_streams/StreamsConsumer4_Map` in Eclipse

## Step 2: Run Producer

Run the `utils.ClickStreamProducer` in Eclipse

Expected output:

Notice `KStream-Action` will only have (action,1)

```console
streams starting on clickstream
map() : got key: facebook.com, value: {"timestamp":1451635200005,"domain":"facebook.com","cost":59,"user":"user_56","campaign":"campaign_6","ip":"2.1.3.9","action":"blocked"}
map() : returning : KeyValue(blocked, 1)
[KSTREAM-MAP-0000000001]: blocked, 1
map() : got key: gmail.com, value: {"timestamp":1451635200010,"domain":"gmail.com","cost":47,"user":"user_53","campaign":"campaign_3","ip":"2.1.3.0","action":"clicked"}
map() : returning : KeyValue(clicked, 1)
[KSTREAM-MAP-0000000001]: clicked, 1
map() : got key: gmail.com, value: {"timestamp":1451635200015,"domain":"gmail.com","cost":94,"user":"user_97","campaign":"campaign_1","ip":"2.2.7.9","action":"blocked"}
map() : returning : KeyValue(blocked, 1)
[KSTREAM-MAP-0000000001]: blocked, 1
```
Stop the consumer

---

## End Lab