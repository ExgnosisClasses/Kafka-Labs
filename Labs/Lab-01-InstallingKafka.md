
<link rel='stylesheet' href='../assets/css/main.css'/>

[<< back to main index](../README.md)

# Lab 1 : Install Kafka

---

### Change Log

Updated 2023-10-28

Rod Davison

---

### Overview

Install and run Kafka

### Depends On

None

### Run time

15 Minutes

## Options for Installing Kafka

### Option 1:  Native install

This guide walks you through installing Kafka **natively** on your machine.  It assumes you have a 'unix like' system (Linux / Mac / Windows with Linux subsystem).

### Option 2: Docker

Another option is to run our docker image.  This image has all the software (Kafka, Spark, etc.) pre-installed and configured.

This assumes that you can run Docker containers on your machine, and you have some basic knowledge of Docker.

Lot of people prefer this, as it has pretty much every thing you need to run the labs with no effort installing and configuring components.

Follow the [docker training image documentation](https://hub.docker.com/r/elephantscale/es-training) for details and instructions.

## Step 1 : Login to your VM

The instructor will provide you with the credentials you need for your VMa and will demonstrate the process for logging into the VM

## Step 2: Download and Install Kafka

Here we are assuming that you are installing kafka in `~/apps/kafka`.  Adjust command paths according to your kafka location.

Use `wget` to download the latest stable version of the Kafka bundle. Alternatively, you can go the Apache Kafka website using the browser in your VM. The provided URL here is the latest stable version of Kafka at the time the lab was prepared.

Extract the Kafka application and rename the folder.

```bash
cd   ~/apps

wget https://downloads.apache.org/kafka/3.6.0/kafka_2.13-3.6.0.tgz

tar xvf kafka_2.13-3.6.0.tgz

mv kafka_2.13-3.6.0 kafka
```

## Step 3: Start Zookeeper

```bash
 ~/apps/kafka/bin/zookeeper-server-start.sh ~/apps/kafka/config/zookeeper.properties
```
Do not close this terminal window that you used to start Zookeeper or else the server will stop running.

## Step 4: Start Kafka

Open a new terminal window to start the Kafka server. In the new window, execute the command below

```bash
JMX_PORT=9999  ~/apps/kafka/bin/kafka-server-start.sh -daemon ~/apps/kafka/config/server.properties
```

We are setting the optional JMX port in order to get metrics easily.

## Step 5: Verify Kafka is Running

Try JPS command to see if Kafka is running

```bash
jps
```

Output will look something like this.  We have Zookeeper and Kafka running

```console
109011 QuorumPeerMain
19363 Kafka
109855 Jps
```

## Extra

Enable deleting the topics.

```bash
echo -e "\n\n delete.topic.enable=true \n" >> ~/apps/kafka/config/server.properties
```

And restart Kafka by stopping and then restarting the server.

```bash
~/apps/kafka/bin/kafka-server-stop.sh
JMX_PORT=9999  ~/apps/kafka/bin/kafka-server-start.sh -daemon  ~/apps/kafka/config/server.properties
```
---

## End Lab