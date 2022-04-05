# pinterest-data-processing-pipeline
An implementation of the pipeline which pinterest uses to process its data  

OVERVIEW

The purpose of this project is to implement the same data pipeline which Pinterest uses to process billions of datapoints every day. 

Firstly, the API is run to take the data and send it to a Kafka topic. This data is then sent simultaneously to 2 different consumers where the pipeline diverges into two paths: one for real time processing where the data is continuously fed in, and the other for batch-processed data which is fed in in chunks at a time.

Real-time processed data first goes to Spark Streaming, then Singlestore(memSQL), then finally monitored with Prometheus and Grafana. 

Batch-processed data is fed into an Amazon S3 bucket, then Spark (at which point, Airflow runs on it daily). From Spark, it gets sent to HBASE, then simultaneously to Presto and finally monitored with Prometheus and Grafana. 
