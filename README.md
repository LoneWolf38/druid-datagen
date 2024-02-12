## Pre Requisities For Druid Datagen


### HDFS Based Batch Ingestion

For HDFS based ingestion have the following file pushed in to HDFS.
  ```
  'https://datasets.clickhouse.com/hits_compatible/hits.tsv.gz'
  ```
1. Download and extract the file in to one of the server where hdfs client is installed
```
wget --no-verbose --continue 'https://datasets.clickhouse.com/hits_compatible/hits.tsv.gz'
gzip -d hits.tsv.gz
```
2. Upload the file to HDFS
```
hdfs dfs -mkdir /data

hdfs dfs -put hits.tsv /data
```

### File Based Batch Ingestion

For File based ingestion just have the following file in one of the servers.

1. Download and extract the file in to one of the server where hdfs client is installed
```
wget --no-verbose --continue 'https://datasets.clickhouse.com/hits_compatible/hits.tsv.gz'
gzip -d hits.tsv.gz
```

### Kafka Streaming Based Ingestion

For Kafka based ingestion, you will require to spin up kafka cluster with 1 or more brokers.
We will use [implydata/druid-datagenerator](https://github.com/implydata/druid-datagenerator)

To deploy the kafka data generator use the following commands
```
docker run -d -p 9999:9999 imply/datagen:latest
```
