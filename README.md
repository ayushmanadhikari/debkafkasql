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

Check to see whether all the conainers are running. 

After all the containers have spun up, we can send a curl request to debezium's connectors endpoint. 
```
curl -H "Accept:application/json" localhost:8083/connectors
```

This gives back the list of up and running connectors. As we have 0 registered connectors, it should give back an empty array as a list of running containers. 

So, we need to register our connector to get it to propagate change data to a kafka topic named "debkafsql_db.debezium.<table_name>". To do that, we need to send another curl request as:

```
curl -i -X POST -H "Accept:application/json" -H "Content-Type:application/json" localhost:8083/connectors/ -d "@debezium_config.json"
```

The ```-d``` tag indicates that the configuration data for the connector is in the ```debezium_config.json``` file.

After sending this request, your connector should be up, running and ready to capture change data. All the tables of the database will now have their separate Kafka topics as "debkafsql_db.debezium.<table_name>" with their respective change data. 





