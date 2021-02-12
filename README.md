# ELK Stack inside Kubernetes.
This is a PoC about running an [ELK stack](https://www.elastic.co/) inside a [Kind](https://kind.sigs.k8s.io/) Kubernetes cluster.

It includes 
* A directory with a random log file. Mounted from the kind host
* Filebeat, reading the previus log file. It outputs to a logstash
* Logstash, processing log lines with an example grok expression, and send it to elastic
* ElasticSearch, the search engine that process log lines
* Kibana, [a window to Elastic Stack](https://www.elastic.co/kibana)

# How to run

First of all you need to create a kind cluster. Please notice there is a log directory mounted from your laptop/desktop.

```
kind create cluster --config cluster.yml
```

We create all pods, deployments and services.
```
kubectl create -f elastic.yml
kubectl create -f logstash.yml
kubectl create -f filebeat.yml
kubectl create -f kibana.yml
```

To access Kibana interface

```
kubectl get pods
...
kubectl port-forward kibana-deployment-... 5601
```