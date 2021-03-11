# Couchbase, Confluent Kafka, and HBase

This covers the following items.
- Setup Couchbase Kafka Connector
- Setup Confluent Platform
- Setup Confluent HBase Connector

## Overview Diagram

![Overview Diagram](./images/cb_confluent_hbase_diagram.jpg)

## Confluent System Requirements

https://docs.confluent.io/current/installation/system-requirements.html

### OS
https://docs.confluent.io/current/installation/system-requirements.html#operating-systems

- RHEL/CentOS 7.x
- RHEL/CentOS 8.x

I confirmed with 7.x.

## Environment
I confirmed with the following environment

- Cloud: AWS

### Confluent
- OS: Red Hat Enterprise Linux (RHEL) 7 (HVM) (RHEL-7.7_HVM-20191119-x86_64-2-Hourly2-GP2)
- Instance Type: t2.xlarge

*Please note that Confluent Platform is resource-intensive. You will fail to register and start HBase Connector without enough memory.*

### Couchbase
- OS: Red Hat Enterprise Linux (RHEL) 7 (HVM) (RHEL-7.7_HVM-20191119-x86_64-2-Hourly2-GP2)
- Instance Type: t2.medium

### Cloudera

You can prepare your Cloudera cluster using the script maintained in my repository, [Single Node CDH Cluster](https://github.com/YoshiyukiKono/SingleNodeCDHCluster).

## Couchbase Setup

In this repository, we assume that you already have a Couchbase cluster to which you will setup Kafka Connector.

Optionally, you may refer to my shell scripts for Couchbase Cluster preparetion on AWS below.

[couchbase-aws-scripts](https://github.com/YoshiyukiKono/couchbase-aws-scripts)

## Instance for Confluent Platform

When you can use shell scripts and AWS CLI, you can use the scripts [here](./scripts/) to create a new EC2 instance.

Otherwise, please create an instance that meets the above specifications, AMI and Instance Type, on your own.

## Cofluent Platform Setup

[1_1_confluent_kafka_setup.md](1_1_confluent_kafka_setup.md)

## Kafka Connector Setup

### Install

[2_1_couchbase_kafka-connector_install.md](2_1_couchbase_kafka-connector_install.md)

### Configuration

[2_2_couchbase_kafka-connector_config.md](2_2_couchbase_kafka-connector_config.md)

### Run Kafka Connector

After you restart your host, you need to run Kafka Connector every time.
```
cd $KAFKA_CONNECT_COUCHBASE_HOME
env CLASSPATH=lib/* \
    connect-standalone.sh $KAFKA_CONNECT_COUCHBASE_HOME/connect-confluent.properties \
                       etc/car-source.properties
```

## HBase Connector Setup

### Configuration

[1_2_conflluent_hbase_connector_setup.md](1_2_conflluent_hbase_connector_setup.md)


### Run Confluent Platform

After you restart your host, you need to run Confluent Platform (No need to register HBase Connector again).
```
$ confluent local start
```

## Check Data Stored in HBase

Login to your Cloudera CDH Cluster and check the data in HBase.

```
$ hbase shell
...
hbase> scan 'cars'
```
Count command returns the number of rows in a table. It’s quite fast when configured with the right CACHE
```
hbase> count 'cars', CACHE => 1000
```
The above count fetches 1000 rows at a time. Set CACHE lower if your rows are big. Default is to fetch one row at a time.


For further details about `hbase shell`, please refer to Apache HBase ™ Reference Guide: https://hbase.apache.org/book.html#shell

You would easily find some other unofficial resources as follows:
- [HBase Shell Commands with Examples](https://www.guru99.com/hbase-shell-general-commands.html)
- [HBase Shell Commands Cheat Sheet](https://sparkbyexamples.com/hbase/hbase-shell-commands-cheat-sheet/)
- [HBase - Shell - Tutorialspoint](https://www.google.com/search?q=hbase+shell+quick+reference&rlz=1C5GCEM_en&oq=hbase+shell+quick+reference&aqs=chrome..69i57.6202j0j7&sourceid=chrome&ie=UTF-8)

## Import data to Couchbase

When you import data to Couchbase, you will find the same data in HBase in real-time.

```
$ cbimport json -c couchbase://127.0.0.1 -u Administrator -p couchbase -b cars -d file://ten_cars.json  -f lines -g '#UUID#'
```

## 
