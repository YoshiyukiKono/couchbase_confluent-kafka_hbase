### Automatic Startup

[Manual Install using Systemd on RHEL and CentOS](https://docs.confluent.io/5.5.0/installation/installing_cp/rhel-centos.html#systemd-rhel-centos-install)

```
sudo rpm --import https://packages.confluent.io/rpm/5.5/archive.key
```

```
cd /etc/yum.repos.d/ 
sudo vi confluent.repo
```
```
[Confluent.dist]
name=Confluent repository (dist)
baseurl=https://packages.confluent.io/rpm/5.5/7
gpgcheck=1
gpgkey=https://packages.confluent.io/rpm/5.5/archive.key
enabled=1

[Confluent]
name=Confluent repository
baseurl=https://packages.confluent.io/rpm/5.5
gpgcheck=1
gpgkey=https://packages.confluent.io/rpm/5.5/archive.key
enabled=1
```

```
sudo yum clean all && sudo yum install confluent-platform-2.12
```

[Using Confluent Platform systemd Service Unit Files](https://docs.confluent.io/current/installation/scripted-install.html)

```
sudo systemctl start confluent-zookeeper
sudo systemctl start confluent-kafka
sudo systemctl start confluent-schema-registry
sudo systemctl start confluent-control-center
sudo systemctl start confluent-kafka-connect
```

```
sudo systemctl stop confluent-zookeeper
sudo systemctl stop confluent-kafka
sudo systemctl stop confluent-schema-registry
sudo systemctl stop confluent-control-center
sudo systemctl stop confluent-kafka-connect
```

```
sudo systemctl status confluent-zookeeper
sudo systemctl status confluent-kafka
sudo systemctl status confluent-schema-registry
sudo systemctl status confluent-control-center
sudo systemctl status confluent-kafka-connect
```
