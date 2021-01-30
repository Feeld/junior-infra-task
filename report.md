# Junior infrastructure task
*Author: Martin Infante*

In this report I will evaluate several monitoring services based on various
criterias and will recommend one of them to be deployed on the system.

## Understanding the requirements
The platform is built around Kubernetes on Google Cloud Platform and it is
integrated with Postgres, Redis, RabbitMQ and MongoDB.
Postgres and MongoDB are two databases, relational and non relational
respectively.
Redis is an in-memory data structure and can be used as a database, cache and
message broker.
RabbitMQ is a message broker that can be used to send messages to many
consumers or to distribute tasks among workers.

## The candidates
There are two main types of candidates to fulfill this
task. Self-hosted and SaaS:

### Self-hosted

* Icinga
* Zabbix
* Prometheus

### SaaS

* New Relic
* Google Cloud Stackdriver
* OpsGenie
* Datadog

A brief description of each of them will be provide next.

## Icinga

Icinga is a monitoring system which checks the availability of the network
resources, notifies users of outages and generates performance data for
reporting. It allows the user to monitor public cloud providers including
Google Cloud Platform and easily scale like the cloud does.
The monitorization of a Kubernetes cluster is not built-in on Icinga, but there
are third
party collaborators that have written some plugins in order to accomplish that
goal.
Postgres, MongoDB and RabbitMQ can also be monitored using Icinga.

### Advantages:

* Scalability.
* Easy integration with GCP.

### Disadvantages:

* Rely on third party plugins to monitor a Kubernetes cluster.

## Zabbix

Zabbix is a monitoring solution for network and application monitoring. It can
configured as a  highly available and scalable service, with security features
already integrated on it.
It can monitor Google Cloud Platform services, but the official documentation
on how to do it is poor.
The monitorization of a Kubernetes cluster requires third party applications.
Postgres, Redis, and RabbitMQ monitoring is supported by Zabbix. MongoDB
requires third party templates.

### Advantages:

* Scalability.
* High availability.
* Security.

### Disadvantages:

* GCP monitoring integration may not be easy.
* Rely on third party applications for Kubernetes and MongoDB monitorization.


## Prometheus

Prometheus is a systems and service monitoring system. The system can run on a
High availability configuration with multiple replicas. It collects metrics
from configured targets at given intervals, evaluates rule expressions,
displays the results and can trigger alarms.
It can be easily integrated with Google Cloud Platform and can be configured to
monitor Kubernetes clusters.
Postgres, Redis, MongoDB, and RabbitMQ can also be monitored with third party
exporters.

### Advantages:

* Easy integration with GCP.
* Kubernetes Monitorization.
* High availabilty.

### Disadvantages:

* Rely on third party exportes for the rest of the services involved.

## New Relic

New Relic is an observability platform that helps the user to monitorize the
activity of their apps and respond faster to failure. It supports native
integration with various Google Cloud Platform services, including the Google
Kubernetes Engine.
Postgress, Redis, MongoDB and RabbitMQ can also be integrated with the New
Relic system.
Pricing is based on the ammount of data ingested by the system.

### Advantages:

* Easy integration with GCP.
* Easy Kubernetes integration.
* Easy integration with the rest of the components.

### Disadvantages:

* Costs can increase fast depending on the system size.

## Google Cloud Stackdriver

Google Clouds's operations suite (formerly Stackdriver) helps the user monitor,
troubleshoot, and improve application performance running on the Google Cloud
environment. It can get data from the Google Kubernetes Engine and can also be
configured for monitoring some third party applications. Nevertheless MongoDB,
Postgres and RabbitMQ plugins are deprecated and migration to BlueMedora is
advised.
Kubernetes metrics with standart resolution are free of charge.

### Advantages:

* Direct integration with Google Kubernetes Engine.
* Pricing advantages.

### Disadvantages:

* Plugins for some of the components of the application are deprecated.
* Relying on all the services from one provider can make migration really hard.

## OpsGenie

OpsGenie is a modern incident management platform for operating always-on
services. OpsGenie can be integrated with Google Stackdriver acting as a
dispatcher for alerts. It can also be integrated with many other monitoring
tools.
Pricing depends on the type of plan selected and the ammount of users to notify.

### Advantages:

* Easy integration with many monitoring tools.

### Disadvantages:

* Provides less capabilities than the other options.

## Datadog
Datadog is a security and monitoring tool for cloud applications. It can bring
together end-to-end traces, metrics and logs of applications and infrastructure.
It can be integrated with Google Kubernetes Engine to collect node-level and
pod-level metrics from the cluster. To collect these second metrics a
containerized version of the Datadog Agent must be deployed on the cluster.
Datadog has also integrations to collect metrics from Postgres, MongoDB, Redis
and RabbitMQ

### Advantages:

* Easy integration with GKE.
* Easy integration with the rest of the components.
* Detailed documentation.

### Disadvantages:

* Pricing depends on number of hosts and plan. Further analisis must be
  performed.

## Analysis

All the tools have advantages and disadvantages but a decision for one of them
should be made thinking on the current requirements but also on the future ones.
On the side of the self-hosted options, Prometheus is a widely accepted tool for
monitoring Kubernetes clusters and it can be easily integrated with Google Cloud
Platform. The other two options do not have the ease to monitor Kubernetes
Clusters and can be, in this case, consider as inferior choices.
On the side of the SaaS options, the most appealing options are New Relic,
Datadog and Google Cloud Stackdriver. The main difference can be encoutered
on pricing.
While New Relic have an increasing rate base on data analized for all the
monitorized variables and Datadog princing depends on the amount of hosts and
selected services, GCP is free of charge for Kubernetes monitoring and only
produces charges for the BlueMedora incoming data. This can lead to great
differences on pricing.

## Conclusion

My personal recommendation for this case will be Google Cloud Stackdriver. This
service can be easily integrated with a Kubernetes Cluster running on GCP and it
has also an option for monitoring the other components of the application using
BlueMedora service. The pricing advantage can be huge on systems that tend to
scale up. The only downside is that relying on the same service provider for
multiple things could lead to a complicated migration if needed, for example, if
Google Clound services conditions change.
If a self-hosted option is prefered, I will recommend Prometheus. It is easily
integrated with Kubernetes Clusters and Google Cloud Platform for monitoring and
it has third party options for monitoring the rest of the components. It is also
widely adopted as a Kubernetes Cluster monitoring tool. It can be configured in
a Highly available configuration, but of course, in contrast to a SaaS, the
possible scalability issues must be taken care of in house.
