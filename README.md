# Dagster Pipes Scala/Spark Demo

This repository is provides a basic example for integration Scala/Spark workloads with dagster-pipes - 
sending logs, check-results, and materialization-results to the dagster orchestrator.

The example Spark workload is based on the official [SparkPi example](https://github.com/apache/spark/blob/master/examples/src/main/scala/org/apache/spark/examples/SparkPi.scala) - that use Map/Reduce to calculate pi on a spark cluster. 

## Running the example with docker

To simplify getting started with scala and spark, see the provided `Dockerfile` and `docker-compose.yml`,
that set up the required environment to build and submit a scala jar to a local Spark cluster.
These are the steps to run the example with docker-compose.

1. Update the values of `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_REGION` environment variables.
1. `docker compose up --build`.
1. Navigate to `localhost:3000`, and click "Materialize Asset".

You should now be able to see your Scala logs, and materialization information in the dagster orchestrator!

## Building the Scala JAR

To build a jar that can be submitted to scala, use the following commands. The resulting jar
will be created at `./external_scala/build/libs/external_scala-all.jar`. In this example, `docker build`
builds the jar.

```
cd ./external_scala
./gradlew build
```

## Submitting the JAR to Spark

```
spark-submit ./external_scala/build/libs/external_scala-all.jar
```