# Couchbase, Confluent Kafka, and HBase

# Diagram

# Requirement

https://docs.confluent.io/current/installation/system-requirements.html

# Setup

## Couchbase

## Confluent Platform


## Configuration
### Couchbase Kafka Connector

### Counfluent HBase Connector

## Run


### Kafka Connector
```
cd $KAFKA_CONNECT_COUCHBASE_HOME
env CLASSPATH=lib/* \
    connect-standalone.sh $KAFKA_HOME/config/connect-confluent.properties \
                       etc/car-source.properties
```

### Confluent HBase Connector
