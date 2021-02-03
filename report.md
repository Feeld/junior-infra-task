# Monitoring tools report for Feeld

This document is an evaluation of the different solutions available in the market to monitor our Kubernetes cluster.

One of the main differences, in terms of monitoring, between monolithic infrastructure and kubernetes, is its difficulty of monotoring. Before microservices, the monitoring of infrastructure was more straight forward. With Kubernetes, the amount of containers created and destroyed, the number of nodes, services deployed within a cluster, the communication between these services and so on, adds a load of complexity into the monitoring system. 

The monitoring systems that served us well before, cannot keep up with the explosion of metrics that these new services entails. The recommended solution in this report, will have to address this complexity in a way that it makes it easier for engineers to manage and understand what is going on in the system as well as helping in the troubleshooting process.

The main goal of our monitoring system will be to enable us to make rational decisions based in data, to respond to incidents and to align the service with our business objectives.

In the microservice world, we need monitoring systems that allow us to alert for high-level services objectives, but retain the granularity to inspect individual components as needed.


## self-hosted or SaaS?

Depending on the requirements of the project one can choose between self-hosted and SaaS monitoring solutions. 

The main difference between them is cost. Self-hosted solutions are usually open source, but that doesn't mean they are free, they come at a cost. Not only the cost of hosting them, but as well the cost of time one has to invest in set-ups in an ongoing bases, specially when such set ups are made up of multiple tools. 

SaaS solutions, in the other hand, usually offer an array of built-in features that help engineers get the data they need without the overhead of configuration. That doesn't mean the don't need to be configured, but probably the time spent in those configurations are less than in a self-hosted one. Of course, they cost money, but depending on the situation, they can be useful if the team wants to get up and running with monitoring but doesn't have much spare capacity for setting them up.

## Requirements

For this project, there are specific requirements for the solutions to integrate with other services: Postgres, Redis, RabbitMQ and MongoDB. As well as the strength, easeness, and reliability to integrate with Kubernetes and GCP.  

These requirements will have a great influence in the selection of the recommended solution.

Another factors like budget allocated to the project or the size of the actual cluster to monitor were excluded from the requirements but will be discussed as well in each of the sections.

## Self-Hosted Solutions


### Prometheus


### Heapster


### Icinga


### Zabbix


## SaaS

### New Relic


### Google Cloud Stackdriver


### DataDog


### Opsgenie


