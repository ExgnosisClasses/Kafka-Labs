<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 2.3: Producing with Keys

---

### Change Log

Updated 2023-10-28

Rod Davison

---

## Overview

Understanding key mappings to partitions

## Run time

10 Minutes

## Step 1: Create Topic  `kv`

```bash
~/apps/kafka/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic kv --replication-factor 1 --partitions 10
```

## Step 2: Create a Comsumer

Create a console consumer using kafkacat

```bash
kafkacat -q -C -b localhost:9092 -t kv -f 'Partition %t[%p], offset: %o, key: %k, value: %s\n'
```

## Step 3: Produce Some key-value pairs

In a different terminal window, use kafkacat to create some messages with keys.

```bash
kafkacat -P -b localhost:9092 -t kv -K :
```

Paste the following values into the producer terminal

```text
A:a1
B:b1
A:a2
C:c1
B:b2
C:c2
D:d1
D:d2
E:e1
F:f1
G:g1
F:f2
A:a3
```

## Step 4: Observe the Consumer Output

The output in the consumer terminal wil resemble this.

```console
Partition kv[2], offset: 2, key: D, value: d1
Partition kv[2], offset: 3, key: D, value: d2
Partition kv[2], offset: 4, key: F, value: f1
Partition kv[2], offset: 5, key: F, value: f2
Partition kv[3], offset: 8, key: B, value: b1
Partition kv[3], offset: 9, key: C, value: c1
Partition kv[3], offset: 10, key: B, value: b2
Partition kv[3], offset: 11, key: C, value: c2
Partition kv[5], offset: 6, key: A, value: a1
Partition kv[5], offset: 7, key: A, value: a2
Partition kv[8], offset: 1, key: E, value: e1
Partition kv[8], offset: 2, key: G, value: g1
Partition kv[5], offset: 8, key: A, value: a3
```

### A few things to note:

- Inspect the partitions for key `A`.  It will always be the same. In the sample output above it is kv[5]; yours might be different partition number.

- Confirm that a specific key will always map to the same partition

- Confirm that more than one key can map to same partition.  In the sample output, keys `D` and `F` both mao to partition 2

## Step 5: Try Sending in More Data

Type in some random data in key-value format, as shown below. Observe how the keys are mapping to the partitions.

```text
customer-1:hi
customer-2:hello
customer-1:bye
customer-2:ciao
zzz:fjsa
yyy:kdfja
```

---

## End Lab