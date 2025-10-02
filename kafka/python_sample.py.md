**kafka-consumer.py**
```
#!/usr/bin/env python3

# Usage:
# pip install kafka-python
# ./consumer.py <my-topic>

# NOTE: only runs for 10 seconds as per consumer_timeout_ms

# See:
# - https://raw.githubusercontent.com/simplesteph/kafka-stack-docker-compose/master/zk-multiple-kafka-multiple.yml
# - https://towardsdatascience.com/getting-started-with-apache-kafka-in-python-604b3250aa05

import sys
from kafka import KafkaConsumer

def main(args):
  try:
    topic = args[0]
  except Exception as ex:
    print("Failed to set topic")

  consumer = get_kafka_consumer(topic)
  subscribe(consumer)


def subscribe(consumer_instance):
    try:
        for event in consumer_instance:
            key = event.key.decode("utf-8")
            value = event.value.decode("utf-8")
            print(f"Message Received: ({key}, {value})")
        consumer_instance.close()
    except Exception as ex:
        print('Exception in subscribing')
        print(str(ex))

def get_kafka_consumer(topic_name, servers=['localhost:9092']):
    _consumer = None
    try:
        _consumer = KafkaConsumer(topic_name, auto_offset_reset='earliest', bootstrap_servers=servers, api_version=(0, 10), consumer_timeout_ms=10000)
    except Exception as ex:
        print('Exception while connecting Kafka')
        print(str(ex))
    finally:
        return _consumer

if __name__ == "__main__":
  main(sys.argv[1:])
```

**kafka-producer.py**
```
#!/usr/bin/env python3

# Usage:
# pip install kafka-python
# ./producer.py <my-topic> <my-key> <my-message>

# See:
# - https://raw.githubusercontent.com/simplesteph/kafka-stack-docker-compose/master/zk-multiple-kafka-multiple.yml
# - https://towardsdatascience.com/getting-started-with-apache-kafka-in-python-604b3250aa05

import sys
from kafka import KafkaProducer

def main(args):
  try:
    topic = args[0]
    key = args[1]
    message = args[2]
  except Exception as ex:
    print("Failed to set topic, key, or message")

  producer = get_kafka_producer()
  publish(producer, topic, key, message)


def publish(producer_instance, topic_name, key, value):
    try:
        key_bytes = bytes(key, encoding='utf-8')
        value_bytes = bytes(value, encoding='utf-8')
        producer_instance.send(topic_name, key=key_bytes, value=value_bytes)
        producer_instance.flush()
        print(f"Publish Succesful ({key}, {value}) -> {topic_name}")
    except Exception as ex:
        print('Exception in publishing message')
        print(str(ex))

def get_kafka_producer(servers=['localhost:9092']):
    _producer = None
    try:
        _producer = KafkaProducer(bootstrap_servers=servers, api_version=(0, 10))
    except Exception as ex:
        print('Exception while connecting Kafka')
        print(str(ex))
    finally:
        return _producer

if __name__ == "__main__":
  main(sys.argv[1:])
```
