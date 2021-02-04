# Monitoring tools report for Feeld

This document is an evaluation of the different solutions available in the market to monitor our Kubernetes cluster.

Kubernetes allows for better development experience but the amount of containers created and destroyed, the number of nodes, services deployed within a cluster, the communication between these services and so on, adds complexity into the monitoring system. 

This explosion of metrics will have to be addressed by the recommended tool in a way that it makes it easier for engineers to manage and understand what is going on in the system as well as helping in the troubleshooting process.

The main goal of our monitoring system will be to enable us to make rational decisions based in data, to respond to incidents and to align the service with our business objectives. 

In the microservice world, we need monitoring systems that allow us to alert for high-level services objectives, but retain the granularity to inspect individual components as needed.

## Self-Hosted or SaaS?

Depending on the requirements of the project one can choose between self-hosted and SaaS monitoring solutions. 

The main difference between them is cost. Self-hosted solutions are usually open source, but that doesn't mean they are free, they come at a cost. Not only the cost of hosting them, but as well the cost of time one has to invest in set-ups in an ongoing bases, specially when such set ups are made up of multiple tools. 

SaaS solutions, in the other hand, usually offer an array of built-in features that help engineers get the data they need without the overhead of configuration. That doesn't mean the don't need to be configured, but probably the time spent in those configurations are less than in a self-hosted one. Of course, they cost money, but depending on the situation, they can be useful if the team wants to get up and running with monitoring but doesn't have much spare capacity for setting them up.

## Requirements

For this project, there are specific requirements for the solutions to integrate with other services: Postgres, Redis, RabbitMQ and MongoDB. As well as the strength, easeness, and reliability to integrate with Kubernetes and GCP.  

These requirements will have a great influence in the selection of the recommended solution.

Another factors like budget allocated to the project or the size of the actual cluster to monitor were excluded from the requirements but will be included in the final decision. 

## Self-Hosted Solutions

### Prometheus - https://prometheus.io/

Prometheus is an open source monitoring and alerting toolkit initially built at Soundcloud. In 2016, joined the Cloud Native Computing Fundation as the second hosted project, after Kubernetes.

Prometheus is a pull-based system. It sends a scrape request based on the configuration defined in the deployment file. The response to this scrape request is stored and parsed in storage along with the metrics for the scrape itself.

The storage is a custom database on the Prometheus server and can handle a massive influx of data. 

Prometheus requires only a scraping endpoint, this way metrics can be pulled from several prometheus instances.

Also pulling its a better way of identifying the health of the service because if the endpoint is not available it's pretty clear the service is not healthy, but if the service doesnt push notifications the reasons might vary and is not as clear its health status. 

If unable to monitor if the container is short lived with the pull endpoint. For that prometheus uses a push gateway notification

**PROS**

* Reliable stand alond and self cotain. It works even if part of the infrastructure is down.
* No extensive set up needed, great community support, low complexity.
* Monitor of Kubernetes cluster node resources out of the box.
* Components available as docker images. Can be easily deployed in container environment
* Integrates with Postgres, Redis, RabbitMQ and MongoDB as well as other [tools](https://prometheus.io/docs/instrumenting/exporters/)

**CONS**

* Difficult to scale. Might need several prometheus servers to collect all the metrics if the applications grows after a certain threshold.
* Step learning curve into how to correctly configure it. As learning promQL, the query language needed to query database of metrics to end up creating Grifana dashboards


### Icinga - https://icinga.com/

Icinga is a monitoring system which checks the availability of your network resources, notifies users of outages, and generates performance data for reporting.

Scalable and extensible, Icinga can monitor large, complex environments across multiple locations.

It has a pluging to connect it to Kubernetes but doesn't seem its used much as it only has 5 downloads. So it would not make it an ideal candidate for our purpose. 


**PROS**


**CONS**
* Does not integrate easily with Kubernetes


### Zabbix - https://www.zabbix.com/

Zabbix is designed to monitor a large number of network parameters and the health of servers, offering many data visualization and reporting features based on the stored data. Small organizations with a few servers and large enterprises with multiple servers can use Zabbix to monitor IT infrastructure.

**PROS**

* Enables you to regularly scan the network for external services or Zabbix agents and take pre-defined actions upon discovery.
* Real-time visualization.

**CONS**
* Does not integrate easily with Kubernetes


### Others

Another tools that were taking into account for this report were Grafana, cAdvisor and FluentD but all of them are related to Prometheus in one way or another. 
cAdvisor, developed by Google, is a tool to analyze mainly individual containers, so it's missing the monitoring capabilities that we need on pods, nodes and other Kubernetes features.
Grafana expands the graphic capabilities of Prometheus and usually is used in conjuntion with it. It can read promQL, the quesy language prometheus uses to send data.
Systemd can also integrate with Prometheus monitoring. 

## SaaS

### New Relic - https://newrelic.com/

New Relic is a web application performance service designed to work in real-time with your live web app. New Relic Infrastructure provides flexible, dynamic server monitoring.

In addition to providing visibility into operational data it also has the ability to see the relationships between objects in a cluster using Kubernetes’ built-in labeling system.

It integrates with GKE and it has a multi-dimensional representation of a Kubernetes cluster from which you can explore your namespaces, deployments, nodes, pods, containers, and applications.

**PROS**

* Able to see the dashboard (kubernetes cluster explorer) with the kubernetes integration. 
* Automatically deployed agent to pods
* Access to kubernetes events
* Troubleshoot without the need of switching tools
* Integrates with Postgres, Redis, RabbitMQ and MongoDB as well as other [tools](https://newrelic.com/integrations).

**CONS**

* Cost $$$$ and it can add up quicly depending on the size of the service.
* It can add load to the cluster as it needs new relic infrastructure to send logs, potentially creating bottle necks.

### Google Cloud Stackdriver

Monitor, troubleshoot, and improve application performance on your Google Cloud environment.

**PROS**

* Already within the GCP stack.
* Integrates with GKE
* It can be integrated with Prometheus.
* Exported metrics from prometheus can be collected in the back end. 
* Paid for storage only.

**CONS**

* Cost $$$$ but it includes all product features for free. Only paying for storage.

### DataDog


### Opsgenie


