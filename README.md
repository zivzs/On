# On
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
