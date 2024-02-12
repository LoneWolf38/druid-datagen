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

## Tuning Druid Related changes


## Application Features
[] Give which type of ingestion job to be performed or all
[] Give the number of iterations to do for the queries to be ran against all the datasources.
[] How many replicas are need for each of the datasource.

### How the application will work

 - `ddgen ingest [kafka | hadoop | file | all]`
   This will perform the ingestion and will keep a state of the application locally, so that if there is any issue then the application will start up at the same point
   All the pre requisites for the ingestion should already be in place otherwise there will be errors which running this command.
 - `ddgen query [--iterations=<number of iterations> --datasource=<datasource>]`
   This will execute the queries against the datasource and will keep a state of the application locally, so that if there is any issue then the application will start up at the same point
 - `ddgen cron [--datasource=<datasource>]`
   This will output a cron expression for you to use in your crontab
