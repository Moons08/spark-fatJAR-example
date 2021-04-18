# Spark build fat-JAR example

[blog post link](https://moons08.github.io/programming/scala_build/)

## requirements

* scala
* sbt
* docker (for spark-submit test)

## build fat-JAR

```shell
$ sbt aseembly
```

## spark-submit test with docker container

```shell
# deploy spark cluster
$ docker-compose up -d

# file copy from local to container
$ docker cp target/scala-2.12/spark-fatJAR-example-assembly-1.0.jar spark-fatjar-example_spark_1:/opt/bitnami/spark/work

# spark-submit (check master IP)
$ docker-compose exec spark ./bin/spark-submit \
  --class buildExample.helloworld \
  --master spark://4f20d2739c84:7077 \
  --executor-memory 1G \
  --total-executor-cores 2 \
  work/spark-fatJAR-example-assembly-1.0.jar
```