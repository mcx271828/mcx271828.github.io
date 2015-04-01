# Kafka Essentials

## Quickstart
Kafka 0.8.2.0

Install:

~~~
tar -xzf kafka_2.10-0.8.2.0.tgz -C /usr/local
ln -s /usr/local/kafka_2.10-0.8.2.0 /usr/local/kafka
~~~

Config:

~~~
vi /usr/local/kafka/config/server.properties
advertised.host.name=<public network ip, not use private network ip>
~~~

Clean old data if neccessary:

~~~
rm -rf /tmp/zookeeper
rm -rf /tmp/kafka-logs
~~~

Run:

~~~
nohup /usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties &
nohup /usr/local/kafka/bin/kafka-server-start.sh /usr/local/kafka/config/server.properties &
~~~

Check status:

~~~
$JAVA_HOME/bin/jps
~~~

Topic management:

~~~
/usr/local/kafka/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test
/usr/local/kafka/bin/kafka-topics.sh --list --zookeeper localhost:2181
~~~

Producer:

~~~
/usr/local/kafka/bin/kafka-console-producer.sh --broker-list <private/public network ip>:9092 --topic test
~~~

Consumer:

~~~
/usr/local/kafka/bin/kafka-console-consumer.sh --zookeeper <usually private network ip>:2181 --topic test --from-beginning
~~~

## Architecture and Design
* [Offical documentation](http://kafka.apache.org/documentation.html)
* [Putting Apache Kafka To Use: A Practical Guide to Building a Stream Data Platform (Part 1)](http://blog.confluent.io/2015/02/25/stream-data-platform-1/)
* [Putting Apache Kafka To Use: A Practical Guide to Building a Stream Data Platform (Part 2)](http://blog.confluent.io/2015/02/25/stream-data-platform-2/)
* [The Log: What every software engineer should know about real-time data's unifying abstraction](http://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)


## Clients
### Producer API
* new Java producer API
* legacy Scala producer API

### Consumer API
* High Level Consumer API
* Simple Consumer API

### Kafka Hadoop Consumer API
linkedin camus

## Performance Test and Tuning


Referneces:

* https://cwiki.apache.org/confluence/display/KAFKA/Performance+testing
* http://engineering.linkedin.com/kafka/benchmarking-apache-kafka-2-million-writes-second-three-cheap-machines
* http://liveramp.com/blog/kafka-0-8-producer-performance-2/

## Cloudera Kafka Integration
* Install CSD
Installation of the CSD will add a new parcel repository to your Cloudera Manager configuration.

~~~
sudo mkdir -p /opt/cloudera/csd
sudo cp KAFKA-1.2.0.jar /opt/cloudera/csd/
sudo /opt/cloudera-manager/cm-5.3.0/etc/init.d/cloudera-scm-server restart
~~~

* Log into the Cloudera Manager Admin Console and restart the Cloudera Management Service
* Download, distribute, and activate the parcel (You do not need to restart the cluster after installing Kafka.)
* add a service

kafka settings:

~~~
log.dirs = /var/local/kafka/data
~~~

Operations:

~~~
sudo kafka-topics --create --zookeeper zookeeper-server:2181 --topic activity --partitions 1 --replication-factor 1
~~~

References:

* http://www.cloudera.com/content/cloudera/en/documentation/cloudera-kafka/latest/topics/kafka.html
* [Install Add-on Services with Custom Service Descriptor Files](http://www.cloudera.com/content/cloudera/en/documentation/core/latest/topics/cm_mc_addon_services.html#concept_qbv_3jk_bn_unique_1)

## Operations
Yahoo Kafka-Manager

References:

* https://github.com/yahoo/kafka-manager
