# Using Confluent's Python Kafka client and librdkafka with Event Hubs for Apache Kafka Ecosystems

This quickstart will show how to create and connect to an Event Hubs Kafka endpoint using an example producer and consumer written in python. Azure Event Hubs for Apache Kafka Ecosystems supports [Apache Kafka version 1.0](https://kafka.apache.org/10/documentation.html) and later.

This sample is based on [Confluent's Apache Kafka Python client](https://github.com/confluentinc/confluent-kafka-python), modified for use with Event Hubs for Kafka.

## Prerequisites

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.

In addition:

* [Git](https://www.git-scm.com/downloads)
* [Python](https://www.python.org/downloads/)
* [Pip](https://pypi.org/project/pip/)
* [OpenSSL](https://www.openssl.org/) (including libssl)
* [librdkafka](https://github.com/edenhill/librdkafka)

Running the setup script provided in this repo will install and configure all of the required dependencies.

## Create an Event Hubs namespace

An Event Hubs namespace is required to send or receive from any Event Hubs service. See [Create Kafka-enabled Event Hubs](https://docs.microsoft.com/azure/event-hubs/event-hubs-create-kafka-enabled) for instructions on getting an Event Hubs Kafka endpoint. Make sure to copy the Event Hubs connection string for later use.

### FQDN

For this sample, you will need the connection string from the portal as well as the FQDN that points to your Event Hub namespace. **The FQDN can be found within your connection string as follows**:

```
Endpoint=sb://{YOUR.EVENTHUBS.FQDN}/;SharedAccessKeyName={SHARED.ACCESS.KEY.NAME};SharedAccessKey={SHARED.ACCESS.KEY}
```

## Set up

Now that you have a Kafka-enabled Event Hubs connection string, clone the Azure Event Hubs for Kafka repository and navigate to the `quickstart/python` subfolder:

```bash
git clone https://github.com/Azure/azure-event-hubs-for-kafka.git
cd azure-event-hubs-for-kafka/quickstart/python
```

Now run the set up script:

```shell
source setup.sh
```

## Producer

### Update the configuration

Update `bootstrap.servers` and `sasl.password` in `producer.py` to direct the producer to the Event Hubs Kafka endpoint with the correct authentication.

### Run the producer from the command line
 
```shell 
python producer.py <topic>
```

Note that the topic must already exist or else you will see an "Unknown topic or partition" error.

## Consumer

### Update the configuration

Update `bootstrap.servers` and `sasl.password` in `consumer.py` to direct the consumer to the Event Hubs Kafka endpoint with the correct authentication.

### Run the consumer from the command line

```shell
python consumer.py <your-consumer-group> <topic.1> <topic.2> ... <topic.n> 
```

## Troubleshooting

This tutorial has a lot of dependencies, so we recommend using the provided setup script. If that doesn't work, here are some potential solutions:

* Run `$ sudo apt-get purge librdkafka1` and rerun the setup script.
* Clone Confluent's python Kafka library from Github and install that instead of the official pip package:

```shell
git clone https://github.com/confluentinc/confluent-kafka-python
pip uninstall confluent-kafka
pip install ./confluent-kafka-python/
```