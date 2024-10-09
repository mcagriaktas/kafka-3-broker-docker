# KAFKA COMMAND

## Create Topic
./kafka-topics.sh --bootstrap-server localhost:9092 --create --topic cagri --replication-factor 3 --partitions 3

## List The Topics
./kafka-topics.sh --bootstrap-server localhost:9092 --list

## Start The Producer
./kafka-console-producer.sh --bootstrap-server localhost:9092 --topic cagri

## Start The Producer with Key and Seperator
./kafka-console-producer.sh --bootstrap-server localhost:9092 --topic cagri --property "parse.key=true" --property "key.separator=,"

## Start The Consumer
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic cagri --from-beginning

## Show Describe The Topic
./kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic cagri

## Delete The Topic
./kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic cagri

## Upgrade The Topic (INCREASE)
./kafka-topics.sh --bootstrap-server localhost:9092 --alter --topic cagri --partitions 5 

##### ==================================================================== #####
##### ==================================================================== #####

## Basic Example
/kafka/bin/kafka-topics.sh \ (1)
--bootstrap-server kafka:9092 \ (2)
--create --topic cagri \ (3)
--replication-factor 3 \ (4)
--partitions 3 (5)


1. This is the script to manage Kafka topics. It is located in the `/kafka/bin`
2. Kafka server's address (check the `/config/server.properties`)
3. This flag is used to create a new topic.
4. This defines the replication factor for the topic, which is the number of Kafka brokers that will replicate the data. (`Not: We deploy 3 broker so our max replication-factor is 3`)
5. This defines the number of partitions for the topic. Each partition allows parallelism in message consumption.

##### ==================================================================== #####
##### ==================================================================== #####

1. ./kafka-topics.sh --bootstrap-server localhost:9092 --create --topic dahbest --replication-factor 3 --partitions 3

2.
    1. terminal-1 = ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic dahbest --from-beginning --partition 0 --property print.key=true
    2. terminal-2 = ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic dahbest --from-beginning --partition 1 --property print.key=true
    3. terminal-3 = ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic dahbest --from-beginning --partition 2 --property print.key=true

3. ./kafka-console-producer.sh --bootstrap-server localhost:9092 --topic dahbest --property "parse.key=true" --property "key.separator=,"

# Output:
## producer terminal
root@805a832ce123:/kafka/bin# ./kafka-console-producer.sh --bootstrap-server localhost:9092 --topic dahbest --property "parse.key=true" --property "key.separator=,"
>1, hellow
>2, I'm Cagri
>3, I'm sure, I am, I
>4, why didnt you send the message to partition 1
>

## terminal-1:
root@0a00f86f4b06:/kafka/bin# ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic dahbest --from-beginning --partition 0 --property print.key=true
>1        hellow

## terminal-2:
root@f87c17deb4f8:/kafka/bin# ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic dahbest --from-beginning --partition 1 --property print.key=true
>4        why didnt you send the message to partition 1

## terminal-3:
root@f87c17deb4f8:/kafka/bin# ./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic dahbest --from-beginning --partition 2 --property print.key=true
>2        I'm Cagri
>3        I'm sure, I am, I
