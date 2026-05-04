\--- title: '\[Doris\] 本機部署Doris' author: Bocky type: post date: 2025-02-06T10:52:03+00:00 url: /2025/02/06/doris-本機部署doris/ categories: - doris ---

資料結構

```
.
├── be_data
├── be_log
├── docker-compose.yml
├── doris-be
├── doris-fe
├── fe_data
└── fe_log
```

docker-compose.yml 內容:

```
# version: '3'
services:
  doris-fe:
    image: selectdb/doris.fe-ubuntu:2.1.6
    container_name: doris_fe
    environment:
      - FE_SERVERS=fe1:10.5.0.2:9010
      - FE_ID=1
    volumes:
      - ./fe_data:/opt/apache-doris/fe/doris-meta
      - ./fe_log:/opt/apache-doris/fe/log
    ports:
      - "8030:8030"  # Web UI
      - "9030:9030"  # MySQL client
      - "9020:9020"  # JDBC
    networks:
      doris_net:
        ipv4_address: 10.5.0.2

  doris-be:
    image: selectdb/doris.be-ubuntu:2.1.6
    container_name: doris_be
    depends_on:
      - doris-fe
    environment:
      - FE_SERVERS=fe1:10.5.0.2:9010
      - BE_ADDR=10.5.0.3:9050
    volumes:
      - ./be_data:/opt/apache-doris/be/storage
      - ./be_log:/opt/apache-doris/be/log
    ports:
      - "8040:8040"
    networks:
      doris_net:
        ipv4_address: 10.5.0.3

networks:
  doris_net:
    driver: bridge
    ipam:
      config:
        - subnet: 10.5.0.0/24
```

docker-compose.yml儲存後下指令

```
docker compose up -d
```

運行成功後進入FE容器中：

```
mysql -h 127.0.0.1 -P 9030 -u root
```

```
-- 建立資料庫
CREATE DATABASE test_db;
USE test_db;

CREATE TABLE employees (
    emp_id INT,
    name VARCHAR(50),
    department VARCHAR(50),
    salary DECIMAL(10,2)
) ENGINE=OLAP
DUPLICATE KEY(emp_id)
DISTRIBUTED BY HASH(emp_id) BUCKETS 1
PROPERTIES (
    "replication_num" = "1"
);

--建立一筆資料
INSERT INTO employees VALUES (1001, 'John Doe', 'IT', 50000.00);
```

## Doris Web UI

打瀏覽器

```
http://localhost:8030
```

User:root

## GUI – TablePlus連線Doris

使用TablePlus連線資訊如下： 選擇MySQL Host/IP: 127.0.0.1 Port:9030 User:root Database:test_db

設置好後按Test，成功會呈現綠底 ![image](https://hackmd.io/_uploads/Hk_XlGfY1x.png)