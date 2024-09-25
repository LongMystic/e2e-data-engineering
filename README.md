<h2>This project is based on this tutorial in <br>Youtube: https://www.youtube.com/watch?v=GqAcTrqKcrY<br>Github: https://github.com/airscholar/e2e-data-engineering</h2>

- This project is run successfully on Windows 10. In this OS, i've installed Spark and simulated Hadoop.
  To install Spark on Windows, follow this video: https://www.youtube.com/watch?v=FIXanNPvBXM
- To run this project:
  + Step 1: Clone this project: ```git clone https://github.com/LongMystic/e2e-data-engineering```
  + Step 2: Move to this folder: ```cd e2e-data-engineering```
  + Step 3: (Optional) If you want run <i>schema-registry</i>, open <b>docker-compose.yml</b> and uncomment some relevant lines
  + Step 4: Open terminal: run ```docker compose up -d``` to start all containers
  + Step 5: Open <b>localhost:8080</b> to access Airflow UI web. There is a dag called <b>user_automation</b> that produce data to kafka broker.
  + Step 6: Open <b>localhost:9021</b> to access Control Center UI web. This is where you can monitor kafka topics and its messages.
  + Step 7: On terminal, run ```python spark-streams.py``` to create Cassandra keyspace, create Cassandra table, read streaming data from kafka topic and write it to Cassandra table.
  + Step 8: Open another terminal, run ```docker exec -it cassandra cqlsh -u cassandra -p cassandra localhost 9042``` to access Cassandra db. Then run ```SELECT * FROM spark_streams.created_users;``` to see data.
- Note:
  + On step 8, to run it successfully, you may have to change some code inside <b>spark_streams.py</b> :
    + Change value of key "spark.jars.packages" to appropriate spark version and scala version
    + If error relevant to "python" occur, you may have to run command ```export PYSPARK_PYTHON=/path/to/python```
### you may want to execute this command
- spark-submit --master spark://localhost:7077 --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.5.1,com.datastax.spark:spark-cassandra-connector_2.12:3.5.1 spark_stream.py
