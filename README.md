Name: Rahul Baliram Shinde

Reg ID: 221080906

Batch: D

=========================================================================================

Task 1: Setting Up the Environment  
Before building the pipeline, we need to install and configure all required components.  

1.	Install Java
![image](https://github.com/user-attachments/assets/a20d5030-344a-4a3a-aa9a-f086c3994bf0)


2.	Install Apache Zookeeper (for coordination)
a.	Download stable ZooKeeper version
![image](https://github.com/user-attachments/assets/d33a47b9-7713-4951-b1ad-670f26583259)

b.	Extract ZIP to C:\zookeeper.
c.	In C:\zookeeper\conf, copy zoo_sample.cfg to zoo.cfg.
d.	In zoo.cfg, set dataDir=C:\zookeeper\data (create the data directory).
![image](https://github.com/user-attachments/assets/1c986cf8-9e31-4bc9-905c-14d33ab88227)

e.	Start ZK server:
![image](https://github.com/user-attachments/assets/eb1e16de-95d5-498f-8f97-b3bd27f4098c)

f.	Verify zookeeper server 
.\zkCli.cmd -server 127.0.0.1:2181

![image](https://github.com/user-attachments/assets/edfd22b6-b25d-4efa-be4a-4c9bdfe08ba9)

3.	Install Apache Kafka
a.	Install kafka
![image](https://github.com/user-attachments/assets/09062285-416c-4ece-9036-1f035e8524c0)

b.	Extracted Kafka
![image](https://github.com/user-attachments/assets/dac26128-0afa-4544-8eb7-bb8cfbc95c52)

c.	Started Kafka broker and connected to existing running zookeeper on port 2181
![image](https://github.com/user-attachments/assets/e9420d16-fca4-48b3-b2b5-2677313b2bf5)
![image](https://github.com/user-attachments/assets/99c4c313-3764-4ed2-85c5-b121b1af07fd)

d.	Creating topic for verifying Kafka
![image](https://github.com/user-attachments/assets/02c5ceb0-6894-4dfd-a967-33b04860e31e)

4.	 Install Apache Spark (for streaming)
![image](https://github.com/user-attachments/assets/7fcd1a3d-d4ec-4c4e-9a8c-6a70066fc589)

5.	 Install Apache Hive (for SQL querying)
![image](https://github.com/user-attachments/assets/575e4ca9-6f53-4fca-953c-00ba4a0680e7)

![image](https://github.com/user-attachments/assets/2ce74ae5-f992-4884-ad0f-1342e425ae5c)

![image](https://github.com/user-attachments/assets/9d2452d9-45d7-4e00-8650-7d066f09c761)

![image](https://github.com/user-attachments/assets/d74506e3-9545-49cf-baf3-2578b5c9327e)

![image](https://github.com/user-attachments/assets/e12693c4-675c-404f-9cc7-2dc5e3926cca)

![image](https://github.com/user-attachments/assets/f7436372-b80d-4294-9832-3924a1440b3f)

7. Install Apache Pig (for ETL)
![image](https://github.com/user-attachments/assets/1ba53712-b83f-4b61-98c4-a94aef720e3e)

![image](https://github.com/user-attachments/assets/674df4ed-2673-4063-9fa3-2aaea14c7b82)

Starting Zookeeper

![image](https://github.com/user-attachments/assets/f382d713-6aff-4419-944f-8c60ab4a5cf0)

8. Install Apache HBase (for NoSQL storage)

![image](https://github.com/user-attachments/assets/f634eb10-ac23-4452-8ba8-f212f0b5959f)

![image](https://github.com/user-attachments/assets/06b9cf43-71c2-48b2-a621-b95d5dc4cba4)

#Ingest real-time data from multiple sources using Apache Kafka.
Starting Kafka

![image](https://github.com/user-attachments/assets/46386f46-190a-465f-92cd-941db5149335)

![image](https://github.com/user-attachments/assets/aee3864d-d3a2-4884-bbce-34d88caeb684)

 program
from kafka import KafkaProducer
import yfinance as yf
import json
import time

producer = KafkaProducer(
    bootstrap_servers='localhost:9092',
    value_serializer=lambda v: json.dumps(v).encode('utf-8')
)

def stream_to_kafka(symbol):
    print(f" Starting to stream real-time data for {symbol}...")
    while True:
        stock = yf.Ticker(symbol)
        data = stock.history(period="1d", interval="1m")
        if not data.empty:
            current_price = data['Close'].iloc[-1]
            msg = {"symbol": symbol, "price": float(current_price)}
            producer.send('rahul-stock-topic', msg)
            print(" Sent to Kafka:", msg)
        else:
            print(" No data fetched. Retrying in 60s.")
        time.sleep(60)

if __name__ == "__main__":
    stream_to_kafka("AAPL")


![image](https://github.com/user-attachments/assets/c6045574-7b68-4df2-9df0-d4c3765bd3c8)


![image](https://github.com/user-attachments/assets/ad0957cd-8272-4e73-96c7-ee8a35ac2828)

Zookeeper started 

![image](https://github.com/user-attachments/assets/f91c6265-2e3d-41db-927b-b7db9d3a425b)

HBase Zookeeper


![image](https://github.com/user-attachments/assets/936fa9aa-1885-42c7-b433-6754992939e5)










10. 













 





