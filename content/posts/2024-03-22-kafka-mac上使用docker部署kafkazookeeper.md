---
title: '[Kafka] Mac上使用Docker部署kafka+zookeeper'
author: Bocky
type: post
date: 2024-03-22T07:32:14+00:00
url: /2024/03/22/kafka-mac上使用docker部署kafkazookeeper/
categories:
  - Kafka
tags:
  - kafka

---
1.  拉取 kafka & zookeeper image

```
docker pull wurstmeister/kafka
docker pull zookeeper
```

2.  運行zookeeper的container

```
docker run -d --name zookeeper -p 2181:2181 -t zookeeper
```

運行kafka(下方會建立3個docker container) 注意：192.168.999.999為自己本機的ip，請自行手動修改 mac查詢方式:

```
ifconfig | grep "inet"
```

看到的inet有192.168.XXX.XXX就是了!\\\[Uploading file…\_28ywkkhaq\\\]() 參數說明:

*   \-d: 表示在背景運行容器
*   –name: 容器命名
*   \-p: 將容器內部的port分享到本機的prot號，用於kafka的監聽端口
*   \-e KAFKA\_BROKER\_ID=0: 設置環境變量，將Kafka Broker的ID設為0。
*   \-e KAFKA\_ZOOKEEPER\_CONNECT=192.168.999.999:2181 將Kafka與Zookeeper連接。Zookeeper預設的prot是2181
*   \-e KAFKA\_ADVERTISED\_LISTENERS=PLAINTEXT://192.168.999.999:9092:
*   PLAINTEXT:// 使用普通的明文文字傳輸協議。這是設定 Kafka 的廣告偵聽器，也就是 Kafka 伺服器公開給外部用戶端的位址和連接埠。
*   \-e KAFKA\_LISTENERS=PLAINTEXT://0.0.0.0:9092: 設置Kafka監聽的地址和端口。
*   \-t wurstmeister/kafka: 指定使用的image(wurstmeister/kafka 是 Kafka 官方維護的一個鏡像

Kafka0：

```
docker run -d --name kafka0 -p 9092:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=192.168.999.999:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.999.999:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -t wurstmeister/kafka
```

Kafka1：

```
docker run -d --name kafka1 -p 9093:9093 -e KAFKA_BROKER_ID=1 -e KAFKA_ZOOKEEPER_CONNECT=192.168.999.999:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.999.999:9093 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9093 -t wurstmeister/kafka
```

Kafka2：

```
docker run -d --name kafka2 -p 9094:9094 -e KAFKA_BROKER_ID=2 -e KAFKA_ZOOKEEPER_CONNECT=192.168.999.999:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://192.168.999.999:9094 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9094 -t wurstmeister/kafka
```

成功後4個container都顯示Running 進入kafka0的container

```
docker exec -it kafka0 /bin/bash
```

進入bin後創建topic

```
cd /opt/kafka_2.13-2.8.1/bin
kafka-topics.sh --create --zookeeper 192.168.999.999:2181 --replication-factor 3 --partitions 5 --topic TestTopic
```

查看指定 topic

```
kafka-topics.sh --zookeeper 192.168.999.999:2181 --topic TestTopic --describe 
```

![image](https://hackmd.io/_uploads/rk5Uw5tCa.png)節點說明：

```
Topic: TestTopic    TopicId: H-Y_jJv5TFSN-sxQBMnzdg PartitionCount: 5   ReplicationFactor: 3
```

*   Topic: 主題名稱
*   Leader: 主題節點號
*   Replicas: 副本節點有Broker.id = 2、0、1（包括Leader Replica和Follower Replica，且不管是否存活），
*   Isr: 表示存活且同步Leader節點的副本有Broker.id = 2、0、1

查看 topic 集合

```
kafka-topics.sh --zookeeper 192.168.999.999:2181 --list
```

![image](https://hackmd.io/_uploads/ByjwPqKAT.png)生產者和消费者測試，開啟三個終端機， 分別在Broker0上運行一個生產者，Broker1、2上分別運行一個消費者：

```
kafka-console-producer.sh --broker-list 192.168.999.999:9092 --topic TestTopic

kafka-console-consumer.sh --bootstrap-server 192.168.999.999:9093 --topic TestTopic --from-beginning

kafka-console-consumer.sh --bootstrap-server 192.168.999.999:9094 --topic TestTopic --from-beginning
```

左邊輸入的地方會有個> 箭頭符號，代表是生產者，送出後會送到右手邊的消費者![image](https://hackmd.io/_uploads/SkrsccY0T.png)\[1\]: https://hackmd.io/\_uploads/SkrsccY0T.png