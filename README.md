# Streaming Bike Sharing Data with Spark

## about
The idea is to consume the [bike sharing](https://www.satori.com/channels/US-Bike-Sharing-Channel) stream from [Satori](https://www.satori.com/) with Spark Structured Streaming.
The streamed data will be aggregated with spark and visualized with a node.js app.

## setup

### Kafka
The Satori feed is read by the python script `Satori2Kafka.py` which writes each message as json to a kafka topic. Therefore a kafka server needs to be running. On a Mac you can install kafka as simple as `brew install kafka`

### Python
The Code is running on Python 3.5. To install the necessary libraries run
```
pip install -r requirements.txt
```

### Node.js
the visualisation part is done in node.js. So you need node.js and npm installed. 
Run `npm install` in the visualize directory to install the dependencies.

### jupyter
You need a jupyter server running.

## run the code
1. run kafka and make sure to have a topic named `satori-bike` and a topic named `aggr-bike`. (see commands below)
2. Run the Satori2Kafka.py script `python Satori2Kafka.py`
3. open the notebook `structured-streaming-kafka-country` in the notebooks directory and run it.
4. change to the visualize directory and run `node index.js`. 
5. open http://localhost:3001 to see the output.

## commands
* start the kafka service by running `bin/kafka`
* list the registered kafka topics:
```
kafka-topics --list --zookeeper localhost:2181
```
* register a new kafka topic
```
kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic satori-bike
```
* read the kafka stream on the command line:
```
kafka-console-consumer --bootstrap-server localhost:9092 --topic satori-bike --from-beginning
```
* write to the kafka stream from the command line:
```
kafka-console-producer --broker-list localhost:9092 --topic satori-bike
```
