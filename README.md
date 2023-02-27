# debkafkasql
A project to capture real time OLTP database(MySql) changes and populate them into a kafka topic. 

## Project Structure 
There are 3 files in this project out of which 2 are docker-compose files which contain the configuration for necessary services. We are using a total of 6 services namely, MySql, Zookeeper, Kafka, KafkaConnect(debezium), Schema-Registry and KafkaUI. I have divided these services in 2 files so that related services are on a single docker-compose file. The 3rd file is the configuration file for the debezium-mysql connector. 

## How to use this project?

