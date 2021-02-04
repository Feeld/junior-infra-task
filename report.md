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

Another factors like budget allocated to the project or the size of the actual cluster to monitor were excluded from the requirements but will be discussed as well in each of the sections.

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


### Zabbix - https://www.zabbix.com/

### Others

Another tools that were taking into account for this report were Grafana, cAdvisor and FluentD. 

## SaaS

### New Relic


### Google Cloud Stackdriver


### DataDog


### Opsgenie


