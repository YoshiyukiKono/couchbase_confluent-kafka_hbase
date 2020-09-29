# Couchbase, Confluent Kafka, and HBase

## Overview Diagram

![Overview Diagram](./images/cb_confluent_hbase_diagram.jpg)

## Requirement

https://docs.confluent.io/current/installation/system-requirements.html

## Environment
I confirmed with the following environment

- Public Cloud: AWS

### Couchbase
- AMI: RHEL-7.7_HVM-20191119-x86_64-2-Hourly2-GP2
- Instance Type: t2.medium

### Confluent
- AMI: RHEL-7.7_HVM-20191119-x86_64-2-Hourly2-GP2
- Instance Type: t2.xlarge

## Couchbase Setup

[couchbase-aws-scripts](https://github.com/YoshiyukiKono/couchbase-aws-scripts)

## Confluent Platform Setup

[1_kafka_setup.md](1_kafka_setup.md)

## Kafka Connector Setup

### Configuration

[2_configuration_kafka_connector.md](2_configuration_kafka_connector.md)

### Run Kafka Connector

After you restart your host, you need to run Confluent Platform (No need to run Couchbase Server manually).
```
cd $KAFKA_CONNECT_COUCHBASE_HOME
env CLASSPATH=lib/* \
    connect-standalone.sh $KAFKA_HOME/config/connect-confluent.properties \
                       etc/car-source.properties
```

## HBase Connector Setup


### Configuration

[3_setup_hbase_connector.md](3_setup_hbase_connector.md)


### Run Kafka Platform

After you restart your host, you need to run Confluent Platform (No need to register HBase Connector again).
```
$ confluent local start
```

## Check Data Stream

Login to your Cloudera CDH Cluster and check the data in HBase.

```
$ hbase shell
...
> scan 'cars'
```
When you import data to Couchbase, you will find the same data in HBase in real-time.

```
$ cbimport json -c couchbase://127.0.0.1 -u Administrator -p couchbase -b cars -d file://ten_cars.json  -f lines -g '#UUID#'
```
