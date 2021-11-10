# learn-kafka

# 1. Starting Kafka
---------------------------------------------
# Mac OS X - Summary
In summary, for Mac OS X
Install brew if needed: /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Download and Setup Java 11 JDK:

brew tap caskroom/versions
brew cask install java11
Download & Extract the Kafka binaries from https://kafka.apache.org/downloads

Install Kafka commands using brew: brew install kafka

Try Kafka commands using kafka-topics (for example)

Edit Zookeeper & Kafka configs using a text editor

zookeeper.properties: dataDir=/your/path/to/data/zookeeper

server.properties: log.dirs=/your/path/to/data/kafka

Start Zookeeper in one terminal window: zookeeper-server-start config/zookeeper.properties

Start Kafka in another terminal window: kafka-server-start config/server.properties
---------------------------------------------
# Linux - Summary
In summary, for Linux (ex: Ubuntu)
Download and Setup Java 11 JDK:

sudo apt install openjdk-11-jdk
Download & Extract the Kafka binaries from https://kafka.apache.org/downloads

Try Kafka commands using bin/kafka-topics.sh (for example)

Edit PATH to include Kafka (in ~/.bashrc for example) PATH="$PATH:/your/path/to/your/kafka/bin"

Edit Zookeeper & Kafka configs using a text editor

zookeeper.properties: dataDir=/your/path/to/data/zookeeper

server.properties: log.dirs=/your/path/to/data/kafka

Start Zookeeper in one terminal window: zookeeper-server-start.sh config/zookeeper.properties

Start Kafka in another terminal window: kafka-server-start.sh config/server.properties

Important: For the rest of the course, don't forget to add the extension .sh to commands being run
---------------------------------------------
# Windows - Summary
In summary, for Windows
Download and Setup Java 11 JDK

Download the Kafka binaries from https://kafka.apache.org/downloads

Extract Kafka at the root of C:\

Setup Kafka bins in the Environment variables section by editing Path

Try Kafka commands using kafka-topics.bat (for example)

Edit Zookeeper & Kafka configs using NotePad++ https://notepad-plus-plus.org/download/

zookeeper.properties: dataDir=C:/kafka_2.12-2.0.0/data/zookeeper (yes the slashes are inversed)

server.properties: log.dirs=C:/kafka_2.12-2.0.0/data/kafka (yes the slashes are inversed)

# Start Zookeeper in one command line: 
	zookeeper-server-start.bat config\zookeeper.properties

# Start Kafka in another command line: 
	kafka-server-start.bat config\server.properties



Important: For the rest of the course, don't forget to add the extension .bat to commands being run

---------------------------------------------
# 2. Kafka Topics CLI
# Create topic
kafka-topics.bat --zookeeper 127.0.0.1:2181 --topic first_topic --create --partitions 3 --replication-factor 1
# List topic
kafka-topics.bat --zookeeper 127.0.0.1:2181 --list
# Describe topic
kafka-topics.bat --zookeeper 127.0.0.1:2181 --topic first_topic --describe
# Delete topic
kafka-topics.bat --zookeeper 127.0.0.1:2181 --topic second_topic --delete

---------------------------------------------
# 3. Kafka Console Producer CLI
kafka-console-producer.bat --broker-list 127.0.0.1:9092 --topic first_topic

---------------------------------------------
# 4. Kafka Console Consumer CLI
# Read topic from the time console start
kafka-console-consumer.bat --bootstrap-server 127.0.0.1:9092 --topic first_topic
# Read all topics from beginning
kafka-console-consumer.bat --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning

---------------------------------------------
# 4. Kafka Consumer In Group
# Mesages in topic are split to each consumer in group
# Note that offset is commited when messages in topic is read (even use --from-beginning)
kafka-console-consumer.bat --bootstrap-server 127.0.0.1:9092 --topic first_topic --group first-group

---------------------------------------------
# 5. Kafka Consumer Group CLI
# List Consumer Group
kafka-consumer-groups.bat --bootstrap-server localhost:9092 --list
# Describe Consumer Group
kafka-consumer-groups.bat --bootstrap-server localhost:9092 --describe --group first-group

---------------------------------------------
# 6. Resseting Offsets
# Reset to earliest
kafka-consumer-groups.bat --bootstrap-server localhost:9092 --group first-group --reset-offsets --to-earliest --execute --topic first_topic
# Reset shift by (>0 is Forward, <0 is Backward)
 kafka-consumer-groups.bat --bootstrap-server localhost:9092 --group first-group --reset-offsets --shift-by -2 --execute --topic first_topic
 
 ---------------------------------------------
# 7. The CLI has many options, but here are the others that are most commonly used:
# Producer with keys
kafka-console-producer --broker-list 127.0.0.1:9092 --topic first_topic --property parse.key=true --property key.separator=,
> key,value
> another key,another value
# Consumer with keys
kafka-console-consumer --bootstrap-server 127.0.0.1:9092 --topic first_topic --from-beginning --property print.key=true --property key.separator=,

---------------------------------------------
# Conduktor - Kafka GUI
Kafka does not come bundled with a UI, but I have created a software name Conduktor to help you use Kafka visually.

You can download Conduktor here: https://www.conduktor.io/

Conduktor allows you to perform all the administrative tasks on Kafka (such as creating topics, partitions, etc), as well as produce and consume, all from within a desktop application that should work on Windows, Mac, and Linux.

---------------------------------------------
# Configuring Producers and Consumers
# Client Configurations
There exist a lot of options to:

# configure producer: https://kafka.apache.org/documentation/#producerconfigs

# configure consumers:  https://kafka.apache.org/documentation/#consumerconfigs
