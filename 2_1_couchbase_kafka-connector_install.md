# Kafka Connector

## Setup

### Java Install

```
$ sudo yum install -y java-1.8.0-openjdk-devel
```


### Couchbase Kafka Connect Download

```
$ curl -OL https://packages.couchbase.com/clients/kafka/4.0.0/couchbaseinc-kafka-connect-couchbase-4.0.0.zip
$ sudo yum install -y unzip
$ unzip couchbaseinc-kafka-connect-couchbase-4.0.0.zip 
```

### Environment Settings

Set the following environment variables (for example, by adding them to `/etc/pfofile`). The passes would differ depending on where you extracted them.
```
export KAFKA_CONNECT_COUCHBASE_HOME=/home/ec2-user/kafka_connector/couchbaseinc-kafka-connect-couchbase-4.0.0
export PATH=$KAFKA_HOME/bin:$PATH
```


### Source Configuration

```
$ cd $KAFKA_CONNECT_COUCHBASE_HOME
$ vi etc/quickstart-couchbase-source.properties 
```
```
couchbase.bucket=events
couchbase.username=Administrator
couchbase.password=couchbase
```


## Reference

https://docs.couchbase.com/kafka-connector/4.0/quickstart.html

https://docs.couchbase.com/kafka-connector/4.0/release-notes.html
