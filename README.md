# Start the Kafka broker

To start the _Broker run:_

    docker-compose up -d

Open an interactive terminal in the  _Broker_  container:

    docker exec -it broker bash

Navigate to the following directory `/opt/bitnami/kafka/bin`:

    cd opt/bitnami/kafka/bin

Execute the following command:

    kafka-topics.sh --create --bootstrap-server 127.0.0.1:9094 --replication-factor 1 --partitions 1 --topic room_1


Now, let’s test if a producer can send messages to the topic we just created. Run the following command:
	
    kafka-console-producer.sh --bootstrap-server 127.0.0.1:9094 --producer.config /opt/bitnami/kafka/config/producer.properties --topic room_1

Consume messages from a topic:

    kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9094 --consumer.config /opt/bitnami/kafka/config/consumer.properties --topic room_1 --from-beginning

# Data ingestion using Python

    python -m producers --help

Let’s inspect the Kafka command:

    python -m producers kafka --help

Open a new terminal in the root of the project and run:

    python -m producers kafka --host localhost --port 9094 --topic room_1 --partition 0 --file-path ./data/room_1/temperature.csv

Finally, with this **Python CLI application,** you can start different _Producers_ to send data to different topics. For example, start a send data to the topic “_room_2_”:

    python -m producers kafka --host localhost --port 9094 --topic room_2 --partition 0 --file-path ./data/room_1/temperature.csv
