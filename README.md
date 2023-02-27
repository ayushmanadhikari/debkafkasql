# debkafkasql
A project to capture real time OLTP database(MySql) changes and populate them into a kafka topic. 


## Project Structure 
There are 3 files in this project out of which 2 are docker-compose files which contain the configuration for necessary services. We are using a total of 6 services namely, MySql, Zookeeper, Kafka, KafkaConnect(debezium), Schema-Registry and KafkaUI. I have divided these services in 2 files so that related services are on a single docker-compose file. First docker-compose file contains services for Zookeeper, Kafka and KafkaUI. The second file contains configuration for MySql, Schema-Registry and KafkaConnect. And the 3rd file is the configuration file for the debezium-mysql connector. 


## About this project
The requirement that we need to meet for this project is that we need to capture the Change Data (CD) so that we may propagate those changes across our collection of databases. We could also store those change data to preserve the history of the states of the database. In order to achieve this objective, we use debezium source connector for MySql db. What debezium does is identifies the changes and synchronizes it in real time across other applications.  


## How to use this project?
As I mentioned in the project structure, there are a total of 6 services divided into 2 docker-compose files. To get all those services running, issue the following command: 

```docker-compose -f docker-compose.yaml -f docker-compose2.yaml up -d```

What this does is spuns up 6 containers and gets all the required services running. The ```-f``` tag indicates the file flag and the ```-d``` tag runs those containers in a detached mode. 
