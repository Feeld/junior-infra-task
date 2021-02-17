# Monitoring configuration guide

This guide will go through the basic steps to configure new monitoring targets
on Prometheus.

## Sections

* [Prometheus exporters](#exporters)
* [Deploying Prometheus](#prometheus-deployment)
* [Blackbox exporter](#blackbox-exporter)
* [Further steps](#further-steps)

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

## Blackbox exporter

The Blackbox exporter allows blacbox probing of endpoints over HTTP, HTTPS, DNS,
TCP and ICMP. The probing results can be scraped by Prometheus.
Inside the *blackbox_deploy* folder there is a Kubernetes manifest for the
deployment of a blackbox-exporter pod.
*blackbox.yaml* is a configuration file, that allows us to define various tests
to perform on the target.
In order to get Blackbox exporter up and running, the following command must be
executed:

```
kubectl apply -f blackbox-deployment.yaml
```

We can test it as follows:

```
kubectl port-forward --namespace=blackbox-exporter svc/prometheus-blackbox-exporter 9115:9115
```

This will map the blackbox service to [http://localhost:9115](http://localhost:9115)
To test a probe against Feeld website, we can go to the following url:
[http://localhost:9115/probe?module=http_2xx&target=https://feeld.co&debug=true](http://localhost:9115/probe?module=http_2xx&target=https://feeld.co&debug=true)
To start monitoring the website, we must add the Blacakbox exporter as a target
for Prometheus. This can be done by adding a new job on the *scrape_configs*
section of the *prometheus.yaml* configuration file. After that, a new set of
rules must be added on the *rule_files* section.
In this case the rules are specified on the *ssl.rules* file. There is a
warning type rule that let us know whenever the web certificate expiration time
is 30 days or less. There is also an alert type rule that let us know if the
certificate has expired.

## Further steps

Further monitoring checks can be set up for the rest of the system components.
I propose the following:

### HTTP API

* Latency.
* Response time.
* Availability.
* Failure rate.
* Correct status codes.

The previously mentioned Blackbox exporter can be used to measure these metrics.

### Postgres and MongoDB

* Response time.
* Disk usage.
* CPU usage.
* Memory usage.
* Load average.
* Number of active sessions.
* Database locks.

There is a [Postgres exporter](https://github.com/wrouesnel/postgres_exporter) for Prometheus to scrape these metrics.
Similar considerations can be done for MongoDB monitoring. There is also an
[MongoDB exporter](https://github.com/dcu/mongodb_exporter) that Prometheus can scrape.

### Redis

* Latency.
* Instantaneous operations per second.
* Hit rate.
* Memory fragmentation ratio.
* Memory usage.
* Connected slaves.
* Rejected connections count.
* Keyspace misses(number of keys requested that do not exists)

There is a [Redis exporter](https://github.com/oliver006/redis_exporte) that helps Prometheus gather thouse metrics.

### RabbitMQ

* Published in/out messages count.
* Unroutable messages count.
* Number of connections.
* Disk usage.
* Memory usage.
* Queue depth.
* Messages rates.
* Messages unacknowledged count.

There is a [RabbitMQ exporter](https://github.com/kbudde/rabbitmq_exporter) that helps Prometheus scrape thouse metrics.

