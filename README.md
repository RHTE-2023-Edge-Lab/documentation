# Documentation

## Lab description

## What you need to have

* One openshift cluster deployed via RHPDS
* OpenShift GitOps operator installed on this cluster
* ...

## Deployment step by step


### x. Kafka

#### 1. 

#### 2. Test to connect to your kafka topic

Connect to one of your kafka pod
```
oc rsh -n <project> <cluster-name>-kafka-0
```

Create a client.properties file
```
sh-4.4$ cat <<EOF>> /tmp/client.properties
> sasl.mechanism=SCRAM-SHA-512
> security.protocol=SASL_PLAINTEXT
> sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
>   username="<user>" \
>   password="<password";
> EOF
```

Connect to your topic
```
./bin/kafka-console-consumer.sh --bootstrap-server <kafka-bootstrap-service>:9092 --topic <your-topic> --consumer.config /tmp/client.properties 
```