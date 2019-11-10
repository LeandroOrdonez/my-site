---
title: "Continuous aggregation in Kafka Streams"
date: 2019-10-17T10:45:27+02:00
draft: false
---

In this post I show a method to address the computation of the arithmetic mean of an stream of values (say sensor readings) using the Kafka Streams DSL. The estimation of the average in a stream processing setting implies keeping track of other two measurements, namely the count of incoming records and the sum of their corresponding values. Let's consider a Kafka streams application consuming messages from a topic to which the readings of multiple temperature sensors are being posted (`temperature-readings`). The messages from said topic are keyed by the sensor ID, and we want to compute the rolling average of the temperature sensed by each device. 

Let's first create a `KGroupedStream` to group the sensor readings according to their corresponding sensor ID:

```java
final StreamsBuilder builder = new StreamsBuilder();
KStream<String, Double> sourceStream = builder.stream("temperature-readings", 
                                Consumed.with(Serdes.String(), Serdes.Double()));
KGroupedStream<String, Double> perSensorStream = sourceStream.groupByKey();
```

Now we can use the `KGroupedStream::aggregate` method to compute the rolling average on the `perSensorStream` we got above. But before this, according to the Kafka [documentation](https://docs.confluent.io/current/streams/javadocs/org/apache/kafka/streams/kstream/KGroupedStream.html#aggregate-org.apache.kafka.streams.kstream.Initializer-org.apache.kafka.streams.kstream.Aggregator-) this method requires an `Initializer` and an `Aggregator` as arguments:
                       
> The specified `Initializer` is applied once directly before the first input record is processed to provide an initial intermediate aggregation result that is used to process the first record. The specified `Aggregator` is applied for each input record and computes a new aggregate using the current aggregate (or for the very first record using the intermediate aggregation result provided via the Initializer) and the record's value. Thus, aggregate(Initializer, Aggregator) can be used to compute aggregate functions like count (c.f. count()). 

Let's create a POJO to provide such initial aggregation and to hold the intermediate aggregation values:

```java
public class AggregateTuple {
    public String sensorId;
    public Long count;
    public Double sum;
    public Double avg;

    public AggregateTuple() {
    }

    public AggregateTuple(String sensorId, Long count, Double sum, Double avg) {
        this.sensorId = sensorId;
        this.count = count;
        this.sum = sum;
        this.avg = avg;
    }
}
```

Now we need to provide an implementation of the `apply` method for the `Aggregator` argument, which would be in charge of computing a new aggregate from the `key` and `value` of an incoming record and the current `aggregate` of the same key:

```java
public static AggregateTuple temperatureAggregator(
    String key, Double value, AggregateTuple aggregate) {
    aggregate.sensorId = key;
    aggregate.count = aggregate.count + 1; // increment by 1 the current record count
    aggregate.sum = aggregate.sum + value; // add the incoming value to the current sum
    aggregate.avg = aggregate.sum / aggregate.count; // update the average
    return aggregate;
}
```

We can finally call the `aggregate` method on the `perSensorStream`:

```java
KTable<String, AggregateTuple> perSensorAggregate = perSensorStream.aggregate(
    () -> new AggregateTuple("", 0L, 0.0, 0.0), // Lambda expression for the Initializer
    (key, value, aggregate) -> temperatureAggregator(key, value, aggregate), // Lambda expression for the Aggregator
    // we can optionally materialize the resulting KTable:
    Materialized.<String, AggregateTuple, KeyValueStore<Bytes, byte[]>>as("temperature-state-store").withValueSerde(aggregateTupleSerde)
);
```

[Here](https://gist.github.com/LeandroOrdonez/aadca09b9aaa41a3b61c41796f3581d1) you can find a complete version of the relevant code outlined in this post.