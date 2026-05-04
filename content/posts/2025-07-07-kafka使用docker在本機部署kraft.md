---
title: '[Kafka] 使用docker在本機部署KRaft模式 + kafka-ui (簡易版)'
author: Bocky
type: post
date: 2025-07-06T21:09:56+00:00
url: /2025/07/07/kafka使用docker在本機部署kraft/
categories:
  - Docker
  - Kafka
tags:
  - docker
  - kafka
  - kraft
toc: true
---

## 前言  

原本官方文件的簡單範例使用預設網路設定，大部分參數都自動配置，較適合單機測試，但無法與 kafka-ui 等其他服務整合。本篇將介紹如何使用 Kafka KRaft 模式 + kafka-ui，並提供完整的配置說明。 

相關連結：
- [docker-kafka](https://hub.docker.com/r/apache/kafka)
- [dockerdocs](https://docs.docker.net.tw/guides/kafka/)
- [gitHub-kafka-ui](https://github.com/provectus/kafka-ui)
- [kafka:3.9.1 image](https://hub.docker.com/layers/apache/kafka/3.9.1/images/sha256-5862db4a63a6dd7d46fd14771b10a1b39e069c2c47f17d8e4640f960720a0ead)

## 什麼是 KRaft 模式？

KRaft (Kafka Raft) 是 Kafka 的新架構模式，主要特色：

不需要 ZooKeeper：簡化部署和維護  
內建 Controller：metadata 管理更高效  
更好的效能：減少網路延遲和複雜度

快速開始 (推薦使用 docker-compose)  
如果你想快速開始，可以直接跳到 docker-compose.yml 章節。

1. 創建自定義網路

```
docker network create kafka-network
```

2. 部署 Kafka Broker
為什麼選擇 3.9.1 而不是 latest？
版本固定，確保環境一致性，避免 latest 版本可能帶來的不穩定性 

```
docker run -d \
  --name broker \
  --network kafka-network \
  -p 9092:9092 \
  -e KAFKA_NODE_ID=1 \
  -e KAFKA_PROCESS_ROLES=broker,controller \
  -e KAFKA_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093 \
  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://broker:9092 \
  -e KAFKA_CONTROLLER_LISTENER_NAMES=CONTROLLER \
  -e KAFKA_CONTROLLER_QUORUM_VOTERS=1@broker:9093 \
  -e KAFKA_INTER_BROKER_LISTENER_NAME=PLAINTEXT \
  apache/kafka:3.9.1
```

環境變數詳解

| 變數 | 說明 |
|------|------|
| KAFKA_NODE_ID=1 | 節點唯一 ID，KRaft 模式必需 |
| KAFKA_PROCESS_ROLES=broker,controller | 同時扮演 broker 和 controller 角色 |
| KAFKA_LISTENERS=PLAINTEXT://:9092,CONTROLLER://:9093 | 監聽接口：9092（客戶端）、9093（內部管理） |
| KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://broker:9092 | 重要：告訴客戶端如何連接 |
| KAFKA_CONTROLLER_LISTENER_NAMES=CONTROLLER | 監聽器名稱 |
| KAFKA_CONTROLLER_QUORUM_VOTERS=1@broker:9093 | 選舉投票設定 |
| KAFKA_INTER_BROKER_LISTENER_NAME=PLAINTEXT | Broker 間通信協定 |

重要提醒： KAFKA\_ADVERTISED\_LISTENERS 必須使用 broker:9092，不能使用 localhost:9092，否則 kafka-ui 無法連接！

## kafka-ui

```
docker run -d \
  --name kafka-ui \
  --network kafka-network \
  -p 8080:8080 \
  -e KAFKA_CLUSTERS_0_NAME=local \
  -e KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=broker:9092 \
  provectuslabs/kafka-ui:latest
```


環境變數的解說:

| 變數 | 說明 |
|------|------|
| KAFKA_CLUSTERS_0_NAME=local | 集群顯示名稱 |
| KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=broker:9092 | 必須與 KAFKA_ADVERTISED_LISTENERS 一致 |

### 測試是否正常

檢查服務狀態

```
bash# 檢查容器運行狀態
docker ps

# 檢查 kafka-ui 日誌
docker logs kafka-ui

# 檢查 broker 日誌
docker logs broker
```

```
# 進入 Kafka 容器
docker exec --workdir /opt/kafka/bin/ -it broker sh

# 創建測試 Topic
./kafka-topics.sh --bootstrap-server localhost:9092 --create --topic test-topic

# 列出所有 Topics
./kafka-topics.sh --bootstrap-server localhost:9092 --list

# 查看 Topic 詳細資訊
./kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic test-topic
```


測試 Producer/Consumer

```
# 啟動 Producer (會出現 > 提示符)
./kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test-topic
> hello kafka
> this is a test message

# 啟動 Consumer (讀取所有訊息)
./kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test-topic --from-beginning
```

透過 kafka-ui 驗證
開啟瀏覽器訪問：http://localhost:8080
你應該能看到：
* Kafka 集群狀態
* Topics 列表
* 剛才發送的訊息


## docker-compose.yml (推薦方式)

請使用docker-compose.yml來儲存下方內容，  
並下指令docker-compose up即可正常運行

```
version: '3.8'
services:
  broker:
    image: apache/kafka:3.9.1
    container_name: broker
    ports:
      - "9092:9092"
    environment:
      KAFKA_NODE_ID: 1
      KAFKA_PROCESS_ROLES: broker,controller
      KAFKA_LISTENERS: PLAINTEXT://:9092,CONTROLLER://:9093
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://broker:9092
      KAFKA_CONTROLLER_LISTENER_NAMES: CONTROLLER
      KAFKA_CONTROLLER_QUORUM_VOTERS: 1@broker:9093
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
    networks:
      - kafka-network

  kafka-ui:
    image: provectuslabs/kafka-ui:latest
    container_name: kafka-ui
    ports:
      - "8080:8080"
    environment:
      KAFKA_CLUSTERS_0_NAME: local
      KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS: broker:9092
    depends_on:
      - broker
    networks:
      - kafka-network

networks:
  kafka-network:
    driver: bridge
```

啟動服務
```
bash# 啟動所有服務
docker-compose up -d

# 查看服務狀態
docker-compose ps

# 查看日誌
docker-compose logs -f

# 停止服務
docker-compose down
```


查看當前版本

```
docker exec -it broker /opt/kafka/bin/kafka-topics.sh --version
```

輸出範例：  
```
4.0.0
```