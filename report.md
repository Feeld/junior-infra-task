# Monitoring tools report for Feeld

This document is an evaluation of the different solutions available in the market to monitor our Kubernetes cluster.

One of the main differences, in terms of monitoring, between an old school infrastructure and kubernetes, it's the difficulty. Before microservices, the monitoring of infrastructure was more straight forward. With Kubernetes, the amount of containers created and destroyed, the number of nodes, services deployed within a cluster, adds a load of complexity into the monitoring system. The solution recommended in this report, will have to address this complexity in a way that it makes it easier for engineers to manage and understand what is going on in the system as well as helping in the troubleshooting process.

The main goal of our monitoring system will be to enable us to make rational decisions based in data, to respond to an incident and to align the service with our business objectives.

In the microservice world, we need monitoring systems that allow us to alert for high-level services objectives, but retain the granularity to inspect individual components as needed.



