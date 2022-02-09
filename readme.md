## Nessie w/ Iceberg Playground

*need docker and docker-compose installed*

#### Step 1 - Start a Nessie Environment

Open your terminal to the directory with the docker-compose.yml

`docker compose up`

to run latest version of nessie run

`docker compose -f latest-nessie.docker-compose.yml up`

**Optional:** install the nessie cli with `pip install pynessie`

#### Step 2 - Open up Iceberg-Spark Container

Open bash in the spark-iceberg container with the following command.

```
docker-compose run spark-iceberg /bin/bash
```

#### Step 3 - Open up SparkSQL

start spark sql with nessie and iceberg

```bash
spark-sql --packages "org.apache.iceberg:iceberg-spark3-runtime:0.12.1,org.projectnessie:nessie-spark-extensions:0.9.2" --conf spark.sql.extensions="org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions,org.projectnessie.spark.extensions.NessieSparkSessionExtensions" --conf spark.sql.catalog.nessie.uri="http://nessie:19120/api/v1" -- conf spark.sql.catalog.nessie.ref=main  -- conf spark.sql.catalog.nessie.authentication.type=NONE --conf spark.sql.catalog.nessie.catalog-impl=org.apache.iceberg.nessie.NessieCatalog --conf spark.sql.catalog.nessie=org.apache.iceberg.spark.SparkCatalog --conf spark.sql.catalog.nessie.warehouse=$PWD/warehouse
```

Now enjoy trying out Nessie with Iceberg