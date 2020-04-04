+++
title = "Mocking sensor data generator"
date = 2020-04-01T11:44:42+02:00
draft = false
tags = ["kafka", "streams", "iot", "sensor", "data"]
categories = ["Programming", "Data management", "Stream processing"]
+++

{{< figure src="/images/ideas/map0-min.jpg" caption="Photo by [Thor Alvis](https://unsplash.com/@terminath0r) on [Unsplash](https://unsplash.com/photos/dWwZBcjw3GE)" >}}

In case you are ever in need of some toy data to get you started with a data project, or just to test your ideas or implementations, I think you might find the Docker setup in [this repo](https://github.com/LeandroOrdonez/temp-readings-gen/) useful. It allows generating synthetic sensor readings of geolocated temperature data, and posting each record to a Kafka topic. The readings generated follow the format specified in the sample records below:

```
{"timestamp": 1585054952527, "geohash": "u155mz82dv33", "sensorId":"s000001", "temp_val": 20.3, "temp_unit": "c"} 
{"timestamp": 1585080280353, "geohash": "u155krxynu5s", "sensorId":"s000002", "temp_val": 19.7, "temp_unit": "c"}
{"timestamp": 1585080335267, "geohash": "u155mz827m6q", "sensorId":"s000010", "temp_val": 24.6, "temp_unit": "c"}
{"timestamp": 1585080366564, "geohash": "u155krxynuhu", "sensorId":"s000007", "temp_val": 17.2, "temp_unit": "c"}
{"timestamp": 1585080388268, "geohash": "u155mz827v2n", "sensorId":"s000004", "temp_val": 22.2, "temp_unit": "c"}
```

## Usage

At least one running instance of Kafka and Zookeeper are required for the generator script to run. Optionally, we provide a `docker-compose` file for deploying a testing Kafka environment in your local machine (based on the `wurstmeister`'s [kafka-docker](https://github.com/wurstmeister/kafka-docker/blob/master/docker-compose-single-broker.yml) deployment). To use it, run:

```
docker-compose -f docker-compose-kafka.yml up -d
```

Once this environment is up, you can spawn the Docker container where the generator script is going to run, and optionally specify some environment variables, such as the bounding box (`BBOX`) within which the temperature readings are going to be located (as a comma-separated sequence of coordinates: `<north>,<west>,<south>,<easth>`), as well as a reference temperature value (`AVG_TEMP`) the generated readings are going to oscillate around (in Celsius degrees):

```
docker run -it \
    --network="host" \
    -e KAFKA_BROKER="localhost:9092" \
    -e BBOX="51.32288838086245,4.091720581054688,51.1509246836981,4.752960205078125" \
    -e AVG_TEMP=19.0 \
    -e KAFKA_TOPIC="temperature-readings" \
    -e RND_SEED="0.0" \
    temp-readings-gen
```

In case you already have a running Kafka setup, omit the `--network="host"` argument, and set the correspondent url (or urls) to the `KAFKA_BROKER` environment variable.

Now you should be able to consume the readings being posted to the `temperature-readings` topic. You can test this by accessing the Kafka Docker container (or by `ssh` into the broker of your existing Kafka setup) and running the following command:

```
kafka-console-consumer.sh \
    --bootstrap-server localhost:9092 \
    --topic temperature-readings \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.StringDeserializer
```

Below you can see the time-series chart of the typical values generated throughout one day:

{{< figure src="/images/ideas/daily-temp-fluctuation.png" class="center" caption="Time-series chart of the generated temperature values" >}}

And there you go, a running network of mobile sensors generating mock temperature data and pushing it into a Kafka topic. You can use this Docker setup to try, for instance, the Kafka streams application we discussed in a [previous post](https://leandro.ordonez.tech/ideas/continuous-aggregation-kafka-streams/), allowing the continuous aggregation of a stream of sensor data. 

