# Configuration - Couchbase Kafka Connector

You need to know the following items. 

- the ip address of your Confluent Platform reachable from Kafka Connector (on Couchbase Server).
- Kafka topic name
- Couchbase user and password
- Couchbase bucket name

## Source Property Configuration
Copy a default peoperties file for your settings.

```
cd $KAFKA_CONNECT_COUCHBASE_HOME
cp etc/quickstart-couchbase-source.properties etc/car-source.properties
```
Edit your property file.

```
vi etc/car-source.properties
```
Change the values of the following properties.
```
# two connectors with the same name will fail.
name=cars-couchbase-source

...

# Publish to this Kafka topic.
couchbase.topic=cars

# Connect to this Couchbase cluster (comma-separated list of bootstrap nodes).
couchbase.seed.nodes=127.0.0.1

...

# Read from this Couchbase bucket using these credentials.
# If the KAFKA_COUCHBASE_PASSWORD environment variable is set,
# it will override the password specified here.
couchbase.bucket=cars
couchbase.username=Administrator
couchbase.password=couchbase
```

## Distination Property File

Copy a default peoperties file for your settings.
```
cp  $KAFKA_HOME/config/connect-standalone.properties $KAFKA_HOME/config/connect-confluent.properties
vi  $KAFKA_HOME/config/connect-confluent.properties
```

Change the distination
```
#bootstrap.servers=localhost:9092
bootstrap.servers=10.0.0.209:9092
```

## Reference

https://docs.couchbase.com/kafka-connector/4.0/quickstart.html

https://docs.couchbase.com/kafka-connector/4.0/release-notes.html
