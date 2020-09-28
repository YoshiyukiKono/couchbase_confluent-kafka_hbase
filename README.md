# Couchbase, Confluent Kafka, and HBase

## Overview Diagram

![Overview Diagram](cb_confluent_hbase_diagram.jpg)

## Requirement

https://docs.confluent.io/current/installation/system-requirements.html

## Environment
I confirmed with the following environment

- Public Cloud: AWS

[couchbase-aws-scripts](https://github.com/YoshiyukiKono/couchbase-aws-scripts)

### Couchbase
- AMI: RHEL-7.7_HVM-20191119-x86_64-2-Hourly2-GP2
- Instance Type: t2.medium

### Confluent
- AMI: RHEL-7.7_HVM-20191119-x86_64-2-Hourly2-GP2
- Instance Type: t2.xlarge

## Couchbase Setup

## Confluent Platform Setup

[1_kafka_setup.md](1_kafka_setup.md)

## Kafka Connector Setup

### Configuration

[2_configuration_kafka_connector.md](2_configuration_kafka_connector.md)

### Run
```
cd $KAFKA_CONNECT_COUCHBASE_HOME
env CLASSPATH=lib/* \
    connect-standalone.sh $KAFKA_HOME/config/connect-confluent.properties \
                       etc/car-source.properties
```

## HBase Connector Setup

[3_setup_hbase_connector.md](3_setup_hbase_connector.md)
