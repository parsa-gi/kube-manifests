
# Elasticsearch on Kubernetes (k8s) with StatefulSets and Persistent Volumes


This repository contains Kubernetes configuration files to deploy an Elasticsearch cluster, including namespace, config maps, Kibana, as well as setting up StatefulSets and Persistent Volume Claims (PVCs) for storage.
## Pre-requisites
- A running Kubernetes cluster
- kubectl command-line tool installed and set up to interact with your cluster
## Installation
## 1.Create the namespace
```console
kubectl apply -f elasticsearch-namespace.yaml
```
## 2. Apply the ConfigMap
```console
kubectl apply -f elasticsearch_configmap.yaml
```
## 3. Create PVs and PVCs
```console
kubectl apply -f elasticsearch_storageclass.yaml
kubectl apply -f elasticsearch_pv.yaml
kubectl apply -f elasticsearch_pvc.yaml
```
## 4. Deploy Elasticsearch
```console
kubectl apply -f elasticsearch_statefulset.yaml
```
## 5. Create NodePort
```console
kubectl apply -f elasticsearch-nodeport.yaml
```
## 5. Deploy Kibaba
```console
kubectl apply -f kibana.yaml
```

## Accessing the Services
Once everything is up and running you can access your services with the port you gave before in NODEPORT section or you can port-forward services to your local machine to access Kibana and Elasticsearch:

Elasticsearch:
```console
kubectl port-forward service/elasticsearch 9200:9200
```

Kibana:
```console
kubectl port-forward service/kibana 5601:5601
```

## Monitoring and Logging
You can check the status of your pods to ensure everything is running as expected using the following command:

```console
kubectl get pods -n elasticsearch
```
To check the logs of a specific pod, use:
```console
kubectl logs -f [POD_NAME]
```


## Cleaning Up
To remove the deployed stack, use the delete command:
```console
kubectl delete -f elasticsearch-namespace.yaml
kubectl delete -f elasticsearch_configmap.yaml
kubectl delete -f elasticsearch_statefulset.yaml
kubectl delete -f kibana.yaml
```
Note: Be careful with the delete command, as it will delete the services and all data stored in the PVCs.
