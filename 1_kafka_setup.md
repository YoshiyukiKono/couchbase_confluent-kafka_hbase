# Confluent Kafka Setup

https://docs.confluent.io/current/quickstart/ce-quickstart.html

## Java Install
```
sudo yum install -y java-1.8.0-openjdk-devel
```

## Download Confluent

Download Confluent Platform from Confluent web site.

https://www.confluent.io/download/

Provide your name and email and select Download, and then choose the desired format .tar.gz or .zip.

Copy the downloaded file to your server.

Decompress the file. You should have the directories

```
$ tar -zxvf confluent-5.5.1-2.12.tar.gz
$ sudo mv confluent-5.5.1 /opt/
$ cd /op
$ sudo su
# ln -s /opt/confluent-5.5.1/ confluent
```

```
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.262.b10-0.el7_8.x86_64
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=.:$JAVA_HOME/jre/lib:$JAVA_HOME/lib:$JAVA_HOME/lib/tools.jar
export CONFLUENT_HOME=/opt/confluent
export PATH=$PATH:$CONFLUENT_HOME/bin
```

```
source /etc/profile
```

Not necessarily needed.

```
$ confluent-hub install --no-prompt confluentinc/kafka-connect-datagen:latest
Running in a "--no-prompt" mode 
Implicit acceptance of the license below:  
Apache License 2.0 
https://www.apache.org/licenses/LICENSE-2.0 
Downloading component Kafka Connect Datagen 0.3.3, provided by Confluent, Inc. from Confluent Hub and installing into /opt/confluent/share/confluent-hub-components 
Adding installation directory to plugin path in the following files: 
  /opt/confluent/etc/kafka/connect-distributed.properties 
  /opt/confluent/etc/kafka/connect-standalone.properties 
  /opt/confluent/etc/schema-registry/connect-avro-distributed.properties 
  /opt/confluent/etc/schema-registry/connect-avro-standalone.properties 
 
Completed 
```
## Usage

### Start Confluent Services

Note: the command sample (`confluent local services start`) in the [QUick Start](https://docs.confluent.io/current/quickstart/ce-quickstart.html) did not work.
```
$ confluent local start
```

Navigate to the Control Center web interface at http://localhost:9021/ and select your cluster.

Select Topics from the cluster submenu and click Add a topic.

Create a topic named `cars` and click Create with defaults.

## Apache HBase Sink Connector

https://docs.confluent.io/current/connect/kafka-connect-hbase/index.html
```
$ confluent-hub install confluentinc/kafka-connect-hbase:latest
The component can be installed in any of the following Confluent Platform installations: 
  1. /opt/confluent (based on $CONFLUENT_HOME) 
  2. /opt/confluent (where this tool is installed) 
Choose one of these to continue the installation (1-2): 1
Do you want to install this into /opt/confluent/share/confluent-hub-components? (yN) y

 
Component's license: 
Confluent Software Evaluation License 
https://www.confluent.io/software-evaluation-license 
I agree to the software license agreement (yN) y

Downloading component Kafka Connect Apache HBase Sink Connector 1.0.5, provided by Confluent, Inc. from Confluent Hub and installing into /opt/confluent/share/confluent-hub-components 
Detected Worker's configs: 
  1. Standard: /opt/confluent/etc/kafka/connect-distributed.properties 
  2. Standard: /opt/confluent/etc/kafka/connect-standalone.properties 
  3. Standard: /opt/confluent/etc/schema-registry/connect-avro-distributed.properties 
  4. Standard: /opt/confluent/etc/schema-registry/connect-avro-standalone.properties 
  5. Based on CONFLUENT_CURRENT: /tmp/confluent.3sl78wkr/connect/connect.properties 
Do you want to update all detected configs? (yN) y

Adding installation directory to plugin path in the following files: 
  /opt/confluent/etc/kafka/connect-distributed.properties 
  /opt/confluent/etc/kafka/connect-standalone.properties 
  /opt/confluent/etc/schema-registry/connect-avro-distributed.properties 
  /opt/confluent/etc/schema-registry/connect-avro-standalone.properties 
  /tmp/confluent.3sl78wkr/connect/connect.properties 
 
Completed 
```

```
[ec2-user@ip-10-0-0-209 ~]$ confluent local load hbase -- -d hbase-qs.json
    The local commands are intended for a single-node development environment
    only, NOT for production usage. https://docs.confluent.io/current/cli/index.html

[ec2-user@ip-10-0-0-209 ~]$ 
```

```
$ confluent local start connect
    The local commands are intended for a single-node development environment
    only, NOT for production usage. https://docs.confluent.io/current/cli/index.html

Using CONFLUENT_CURRENT: /tmp/confluent.3sl78wkr
zookeeper is already running. Try restarting if needed
kafka is already running. Try restarting if needed
schema-registry is already running. Try restarting if needed
Starting connect
connect is [UP]
```


## JQ

https://snapcraft.io/install/jq/rhel
