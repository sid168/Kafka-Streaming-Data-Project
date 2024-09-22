# Kafka-Streaming-Data-Project
This project demonstrates how to work with real-time streaming data using Apache Kafka. You'll configure Kafka to use KRaft mode, set up a message broker, create a topic, and build a producer and consumer for sending and receiving messages.



## Project Goals

- Download and extract Kafka binaries.
- Configure Kafka to use KRaft mode.
- Start the Kafka message broker service. (The broker is the part of Kafka that stores and manages the messages (data). "Starting the broker" means you're turning on Kafka’s engine to begin receiving, storing, and sending messages.
Without the broker running, no messages can be sent or received, so this step is like turning on the main part of the system.)

- Create a topic.
- Build and start a producer to send messages.
- Build and start a consumer to receive messages.

---

## Steps

### **Step 1: Download and Extract Kafka**

1. **Open a terminal**:
   - Start a new terminal session.

2. **Download Kafka binaries**:
   - Download the latest version of Kafka using the following command:
     ```bash
     wget https://downloads.apache.org/kafka/3.8.0/kafka_2.13-3.8.0.tgz
     ```

3. **Extract the Kafka archive**:
   - Extract the downloaded archive with the following command:
     ```bash
     tar -xzf kafka_2.13-3.8.0.tgz
     ```
   - This will create a directory `kafka_2.13-3.8.0`.

---

### **Step 2: Configure KRaft Mode and Start Kafka Server**

1. **Navigate to the Kafka directory**:
   - Move to the Kafka directory with:
     ```bash
     cd kafka_2.13-3.8.0
     ```

2. **Generate a unique Cluster ID**:
   - Use the following command to generate a unique Cluster ID:
     ```bash
     KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"
     ```

3. **Configure log directories**:
   - Format the log directories using the Cluster ID:
     ```bash
     bin/kafka-storage.sh format -t $KAFKA_CLUSTER_ID -c config/kraft/server.properties
     ```

4. **Start the Kafka server**:
   - Start the server with:
     ```bash
     bin/kafka-server-start.sh config/kraft/server.properties
     ```

---

### **Step 3: Create a Topic and Start a Producer**



1. **Create a new topic**:
   - Before sending messages, create a Kafka topic called `personal_updates`:
     ```bash
     bin/kafka-topics.sh --create --topic personal_updates --bootstrap-server localhost:9092
     ```
A topic is like a mailbox or folder where you store specific types of messages. When you create a topic, you’re making a space in Kafka where certain messages will go.
Topics organize data, so creating a topic is essential for sending or receiving messages in an organized way.

2. **Start a producer**:
   - Start the producer that will send messages to the `personal_updates` topic:
     ```bash
     bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic personal_updates
    ```
    A producer is a program that creates and sends messages to Kafka. "Starting a producer" means you’re launching the program that will start sending data.
Without a producer, there would be no messages to send into the system for others to read.

3. **Send some custom messages**:
   - Once the producer is running, type the following personalized messages and press enter after each:
     ```
     Starting my Kafka project
     Real-time data is so powerful!
     Excited to explore more with Kafka
     ```

---

### **Step 4: Start a Consumer**

1. **Start a consumer**:
   - Open a new terminal and navigate to the Kafka directory again:
     ```bash
     cd kafka_2.13-3.8.0
     ```
   - Run the following command to start the consumer and listen to the `personal_updates` topic:
     ```bash
     bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic personal_updates --from-beginning
     ```
A consumer is a program that reads messages from Kafka. "Starting a consumer" means you’re launching the program that will start receiving and reading the messages.
Consumers are how we actually use the messages sent into Kafka. Without them, no one would be able to read or process the messages being sent.

2. **Verify the messages**:
   - You should see the messages you sent from the producer appear here:
     ```
     Starting my Kafka project
     Real-time data is so powerful!
     Excited to explore more with Kafka
     ```

---

### **Step 5: Explore Kafka Directories**

1. **List the directories**:
   - Open a new terminal, navigate to the Kafka directory, and list its contents:
     ```bash
     cd kafka_2.13-3.8.0
     ls
     ```

2. **View message logs**:
   - Kafka stores logs in `/tmp/kraft-combined-logs/`. To view the logs for the `personal_updates` topic, run:
     ```bash
     ls /tmp/kraft-combined-logs/personal_updates-0
     ```

---

### **Step 6: Clean Up**

1. **Stop the producer**:
   - In the terminal where the producer is running, press `CTRL + C`.

2. **Stop the consumer**:
   - In the terminal where the consumer is running, press `CTRL + C`.

3. **Stop the Kafka server**:
   - In the terminal running the Kafka server, press `CTRL + C`.

