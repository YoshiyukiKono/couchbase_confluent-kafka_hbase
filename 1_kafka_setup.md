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
