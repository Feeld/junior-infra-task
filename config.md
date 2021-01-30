# Monitoring configuration guide

This guide will go through the basic steps to configure new monitoring targets
on Prometheus.

## Sections

* [Prometheus exporters] (Exporters)
* [Deploying Prometheus] (Prometheus deployment)
* [Blackbox exporter] (Blackbox exporter)
* [Further steps] (Further steps)

## Exporters

The exporters are a variety of libraries which help in exporting existing
metrics from third-party systems as Prometheus metrics. They are helpful for
cases where it is not feasible to instrument a given system with Prometheus
metrics directly.
There are a number of exporters that are maintained as part of the official
[Prometheus Github organization](https://github.com/prometheus) and are marked
as official, and others that are externally contributed and maintained.

## Prometheus deployment

Inside the *prometheus_deploy* folder there are a number of *yaml* kubernetes
manifests which are used to deploy a Prometheus cluster to Kubernetes.
*prometheus.yaml* is an important configuration file for Prometheus, which
allows the user to configure, for example, the scrape interval, jobs for adding
new targets, rules files.
*node-exporter-daemonset.yaml* is an exporter that allows Prometheus to get
metrics about pods and nodes in the cluster.
In order to get Prometheus up and running, the following commands must be
executed in order:

```
kubectl apply -f prometheus-namespace.yaml # creates a 'prometheus' namespace
kubectl apply -f prometheus-config.yaml
kubectl apply -f prometheus-roles.yaml
kubectl apply -f prometheus-deployment.yaml # creates prometheus pod
kubectl apply -f prometheus-nodeservice.yaml # Exposes prometheus service
kubectl apply -f node-exporter-daemonset.yaml # Deploys the node exporter
```
*Note*: These files can be combined into one yaml file. They were splited for
the purpose of the task. 
