<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 4.2: Compression

---

### Change Log

Updated 2023-10-28

Rod Davison

---

### Watch and Do

The instructor will do a demo of this lab before you try it  on your own 

### Overview

Enable compression on Producer

### Depends On

None

### Run time

15 Minites

## Step 1 : Create `testc` topic


```bash
~/apps/kafka/bin/kafka-topics.sh  --bootstrap-server localhost:9092  --create --topic testc --replication-factor 1  --partitions 2
```

## Step 2: Run a console consumer

In a terminal run either the standard Kafka consumer shown below

```bash
~/apps/kafka/bin/kafka-console-consumer.sh \
        --bootstrap-server localhost:9092 \
        --property print.key=true --property key.separator=":" \
        --topic testc
```

Or run Kafkacat

```bash
kafkacat -q -C -b localhost:9092 -t testc -f 'Partition %t[%p], offset: %o, key: %k, value: %s\n'
```

## Step 3: Compression Producer

In Eclipse, open the file  `src/main/java/x/lab04_benchmark/CompressionProducer.java`.

Run the Producer in Eclipse
  In Eclipse, 
- Right click on `src/main/java/x/lab04_benchmark/CompressionProducer.java`
- Run as 'Java Application'

In Eclipse console, you should see output as follows:

```console
Sent record [1] (key:1698588562682, value:Hello world @ 1698588562682), meta (partition=0, offset=19, timestamp=1698588562813), time took = 216.64 ms
Sent record [2] (key:1698588562683, value:Hello world @ 1698588562683), meta (partition=1, offset=11, timestamp=1698588562898), time took = 1.64 ms
Sent record [3] (key:1698588562684, value:Hello world @ 1698588562684), meta (partition=0, offset=20, timestamp=1698588562900), time took = 1.02 ms
```

## Step 4: Monitor Kafka console consumer

Confirm that the messages have been read by the console consumer

---

## End Lab