# Setup monitoring on Kubernetes Cluster using Prometheus and Grafana

- Prometheus server - Processes and stores metrics data

- Grafana - Visualize scraped data in UI

## Pre-requisites:
- Kubernetes Cluster
- Helm

## Setup Process:

1. Check Helm
```bash
helm version
```
2. Add helm stable chart
```bash
helm repo add stable https://charts.helm.sh/stable
```
3. Add Prometheus repo
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
check helm repo list
```bash
helm repo list
```
4. Search repo
```bash
helm search repo prometheus-community
```
5. Create a namespace for prometheus
```bash
kubectl create namespace prometheus
```
6. Install prometheus-community/kube-prometheus-stack
```bash
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
```
7. Check pods in prometheus namespace
```bash
kubectl get pods -n prometheus
```
8. Check services in prometheus namespace
```bash
kubectl get svc -n prometheus
```
9. Now need to expose the ip to access outside of the cluster. Here let's use NodePort instead of ClusterIP.
```bash
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
```
10. Same for grafana
```bash
kubectl edit svc stable-grafana -n prometheus
```
11. Check svc now
```bash
kubectl get svc -n prometheus
```
### note: make sure both ports are enable to accept inbound request

12. Browse the grafana using cluster ip <ip_address>:port for grafana

Then use below credential and update them. 

UserName: admin 
Password: prom-operator

## Create Dashboard in Grafana.

Find your necessary dashbroad from [here](https://grafana.com/grafana/dashboards/). 

copy the ID and import in your grafana. 