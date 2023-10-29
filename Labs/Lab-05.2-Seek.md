<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 5: Seek To Various Offsets

---

### Change Log

Updated 2023-10-28

Rod Davison

---
### Overview

Seek within partition


### Run time

20 Minutes

## Step 1: Run Kafkacat to see offsets and messages

On a terminal, run Kafkacat.  Observe the offsets and messages.

```bash
kafkacat -q -C -b localhost:9092 -t offsets -f 'Partition %t[%p], offset: %o, key: %k, value: %s\n'
```

## Step 2: Seeking Consumer

Open the file `src/main/java/x/lab05_offsets/SeekingConsumer.java`

Notice the TODO items have different variations to try
  
Use reference Java API [for Consumer](https://kafka.apache.org/0100/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html)

Run the producer in Eclipse,
- Right click on file
- Run as 'Java Application'


## Step 3: Work Through TODOs

Observe the behavior with each option selected.

---

## End Lab