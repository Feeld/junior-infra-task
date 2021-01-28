# Junior infrastructure task
## Author: Martin Infante

In this report I will evaluate several monitoring services based on various criterias and will
recommend one of them to be deployed on the system.

## Understanding the requirements
The platform is built around Kubernetes on Google Cloud Platform and it is integrated with
Postgres, Redis, RabbitMQ and MongoDB.

## The candidates
There are two main types of candidates to fulfill this task. Self-hosted and SaaS:

### Self-hosted

* Icinga
* Zabbix
* Prometheus

### SaaS

* New Relic
* Google Cloud Stackdriver
* OpsGenie

A brief description of each of them will be provide next.

## Icinga

Icinga is a monitoring system which checks the availability of the network resources, notifies
users of outages and generates performance data for reporting. It allows the user to monitor
public cloud providers including Google Cloud Platform and easily scale like the cloud does.
The monitorization of a Kubernetes cluster is not easily done with Icinga, but there are third
party collaborators that have written some applications in order to accomplish that goal.
Postgres, MongoDB and RabbitMQ can also be monitored using Icinga.

### Advantages:

* Scalability.
* Easy integration with GCP.

### Disadvantages:

* Rely on third party applications to monitor a Kubernetes cluster.

## Zabbix

Zabbix is a monitoring solution for network and application monitoring. It can configured as a 
highly available and scalable service, with security features already integrated on it.
It can monitor Google Cloud Platform services, but the official documentation on how to do
it is poor.
The monitorization of a Kubernetes cluster requires third party applications.
Postgres, Redis, and RabbitMQ monitoring is supported by Zabbix. MongoDB requires
third party templates.

### Advantages:

* Scalability.
* High availability.
* Security.

### Disadvantages:

* GCP monitoring integration may not be easy.
* Rely on third party applications for Kubernetes and MongoDB monitorization.


## Prometheus

Prometheus is a systems and service monitoring system. The system can run on a High availability
configuration with multiple replicas. It collects metrics from configured targets at given
intervals, evaluates rule expressions, displays the results and can trigger alarms.
It can be easily integrated with Google Cloud Platform and can be configured to monitor
Kubernetes clusters.
Postgres, Redis, MongoDB, and RabbitMQ can also be monitored with third party exporters.

### Advantages:

* Easy integration with GCP.
* Kubernetes Monitorization.
* High availabilty.

### Disadvantages:

* Rely on third party exportes for the rest of the services involved.

## New Relic

New Relic is an observability platform that helps the user to monitorize the activity of their
apps and respond faster to failure. It supports native integration with various Google Cloud
Platform services, including the Google Kubernetes Engine.
Postgress, Redis, MongoDB and RabbitMQ can also be integrated with the New Relic system.
Pricing is based on the ammount of data ingested by the system.

### Advantages:

* Easy integration with GCP.
* Easy Kubernetes integration.
* Easy integration with the rest of the components.

### Disadvantages:

* Further analysis on pricing should be performed.
