# On: queues made simpler

## What is On
On is simple client that help build reactive micro-services architechture on top of queues.
Currently, supporting Java only, but will support many other popular languages.

On provides a way for a developer to define reactors using simple POJOs and simple conditions syntax.

``` java
 @On("payment.processed == false")
 public void processPayment(Payment payment) {
    // Do something with the payment
    payment.processed = true;
    On.post(payment);
    
    //Produce and send receipt
    Reciept receipt = ...;
    On.post(receipt);
}
```

## How On works
It uses your reactors, the files with the @On annotation, to setup a listener on the queue behind  the scenes.
The default queue is an Apache Kafka. But it can be extended to any other queue like RabbitMQ, ApacheMQ, etc...
## Adding On to your build

On's Maven group ID is `io.on` and its artifact ID is `on`.
To add a dependency on On using Maven, use the following:

```xml
<dependency>
  <groupId>io.on</groupId>
  <artifactId>on</artifactId>
  <version>1.0.0</version>
</dependency>
```

To add a dependency using Gradle:

```gradle
dependencies {
  compile 'io.on:on:1.0.0'
}
```

## Initializing on
``` java
 public static void main(String[] args) {
    On on = On.Builder()
        .setQueue(new OnKafkaQueue("localhost:9092"))
        .addReactor(MyReactor1.class)
        .addReactor(MyReactor2.class)
        .build();
        
    on.start();
    ...
  }
```


``` java
public class MyReactor {
 @On("payment.processed == false")
 public void processPayment(Payment payment) {
    // Do something with the payment
    payment.processed = true;
    On.post(payment);
    
    //Produce and send receipt
    Reciept receipt = ...;
    On.post(receipt);
 }
}
```
