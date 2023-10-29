<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 4.1: Producer Benchmarking
---

### Change Log

Updated 2023-10-28

Rod Davison

---
### Overview
Understand different send methods used by Producers

### Depends On
lab 3

### Run time
30 Minutes

## Step 1: Create a benchmark topic

```bash
~/apps/kafka/bin/kafka-topics.sh  --bootstrap-server localhost:9092 --create --topic benchmark --replication-factor 1  --partitions 2
```

## Step 2: Run the Producer

Open the file  `src/main/java/x/lab_04/BenchmarkProducerSendModes.java`

In Eclipse,
- Right click on `src/main/java/x/lab04_benchmark/BenchmarkProducerSendModes.java`
9Run as 'Java Application'

In Eclipse console, you should see output as follows:

```console
== Producer starting.... : Benchmark Producer (topic=benchmark, maxMessages=100,000, sendMode=SYNC)
== Benchmark Producer (topic=benchmark, maxMessages=100,000, sendMode=SYNC) done.  100,000 messages sent in 1,527.884 milli secs.  Throughput : 65,449 msgs / sec
== Producer done.


== Producer starting.... : Benchmark Producer (topic=benchmark, maxMessages=100,000, sendMode=ASYNC)
== Benchmark Producer (topic=benchmark, maxMessages=100,000, sendMode=ASYNC) done.  100,000 messages sent in 16.13 milli secs.  Throughput : 6,199,477 msgs / sec
== Producer done.


== Producer starting.... : Benchmark Producer (topic=benchmark, maxMessages=100,000, sendMode=FIRE_AND_FORGET)
== Benchmark Producer (topic=benchmark, maxMessages=100,000, sendMode=FIRE_AND_FORGET) done.  100,000 messages sent in 9.549 milli secs.  Throughput : 10,472,250 msgs / sec
== Producer done.
```

inspect the throughput numbers for various modes and discuss the findings.


---

## End Lab