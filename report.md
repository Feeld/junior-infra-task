# Monitoring tools report for Feeld

This document is an evaluation of the different solutions available in the market to monitor our Kubernetes cluster.

Kubernetes allows for better development experience but the amount of containers created and destroyed, the number of nodes, pods, services deployed within a cluster and the communication between these services, it adds complexity into the monitoring system. 

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

Another factors like budget allocated to the project or the size of the actual cluster to monitor were excluded from the requirements I believe they play a part as well in the final decision so they will be included in the analysis. 

## Self-Hosted Solutions

### Icinga - https://icinga.com/

Icinga is a monitoring system which checks the availability of your network resources, notifies users of outages, and generates performance data for reporting.

Scalable and extensible, Icinga can monitor large, complex environments across multiple locations.

It has a pluging to connect it to Kubernetes but doesn't seem its used much. There seems to be another connectors as well but the ecosystem is not extensive developed.

**PROS**

* Provides data and alerts for availability, connectivity, and general health checks of your infrastructure.
* It's fast. Quick notifications on system issues thanks to its multithreaded design.
* Uses very similar plugings and add-ons to Nagios.
* 3rd party integrations with MongoDB, Redis, RabbitMQ (Nagios) and Postgres 

**CONS**

* Might need another tool to monitor Kubernetes cluster.
* Although it has a focus in community, there is not a huge amount of info available on how to configure it.  
* Mainly used for static infrastructure.


### Zabbix - https://www.zabbix.com/

Zabbix is designed to monitor a large number of network parameters and the health of servers, offering many data visualization and reporting features based on the stored data. 

Both large and small organizations can use Zabbix to monitor IT infrastructure. It provides monitoring metrics, among others network utilization, CPU load and disk space consumption.

It's capable of storing the data in an array of services. Visualization features are available as well as very flexible ways of analyzing the data and alerting.

**PROS**

* High performance and capability. Able to monitor +100.000 devices.
* Enables you to scan the network for external services and take pre-defined actions upon discovery.
* Strong API integrations which makes it easy to extend.
* Real-time visualization and nice grapahs

**CONS**

* Does not integrate easily with Kubernetes.
* Support sold separetly.
* It can get difficult to configure.
* Not detailed documentation. Difficult for first-timers. 

### Prometheus - https://prometheus.io/

Prometheus is an open source monitoring and alerting toolkit initially built at Soundcloud. In 2016, joined the Cloud Native Computing Fundation as the second hosted project, after Kubernetes.

Works in a pull-based system. It sends a scrape request based on the configuration defined in the deployment file. The response to this scrape request is stored and parsed in storage along with the metrics for the scrape itself.

The storage is a custom database on the Prometheus server and can handle a massive influx of data. 

Prometheus requires only a scraping endpoint, this way metrics can be pulled from several Prometheus instances.

Also pulling its a better way of identifying the health of the service because if the endpoint is not available it's pretty clear the service is not healthy, but if the service doesnt push notifications the reasons might vary and is not as clear its health status. 

If unable to monitor if the container is short lived with the pull endpoint. For that Prometheus uses a push gateway notification

**PROS**

* Reliable stand alond and self cotain. It works even if part of the infrastructure is down.
* No extensive set up needed, great community support, low complexity.
* Monitor of Kubernetes cluster node resources out of the box.
* Components available as docker images. Can be easily deployed in container environment
* Integrates with Postgres, Redis, RabbitMQ and MongoDB as well as other [tools](https://Prometheus.io/docs/instrumenting/exporters/)

**CONS**

* Difficult to scale. Might need several Prometheus servers to collect all the metrics if the applications grows after a certain threshold.
* Step learning curve into how to correctly configure it. As learning promQL, the query language needed to query database of metrics to end up creating Grifana dashboards
* Memory intensive. Can use fair amount of the memory when deployed within the cluster.
* Own graphical interface is lacking. Need to integrate it with dashboard platform like Grifana.

### Others

Another tools that were taking into account for this Self-Hosted list were Grafana, cAdvisor and FluentD. All of them are related to Prometheus in one way or another. 
cAdvisor, developed by Google, is a tool to analyze mainly individual containers, so it's missing the monitoring capabilities that we need on pods, nodes and other Kubernetes features.
Grafana expands the graphic capabilities of Prometheus and usually is used in conjuntion with it. It can read promQL, the quesy language Prometheus uses to send data.
Systemd can also integrate with Prometheus monitoring. 

## SaaS

### New Relic - https://newrelic.com/

New Relic is a web application performance service designed to work in real-time with your live web app. New Relic Infrastructure provides flexible, dynamic server monitoring.

In addition to providing visibility into operational data it also has the ability to see the relationships between objects in a cluster using Kubernetes’ built-in labeling system.

It integrates with GKE and it has a multi-dimensional representation of a Kubernetes cluster from which you can explore your namespaces, deployments, nodes, pods, containers, and applications.

**PROS**

* Able to see the dashboard (kubernetes cluster explorer) with the kubernetes integration. 
* Automatically deployed agent to pods and access to kubernetes events.
* Troubleshoot without the need of switching tools.
* Integrates with Postgres, Redis, RabbitMQ and MongoDB as well as other [tools](https://newrelic.com/integrations).
* Real time reports.

**CONS**

* Cost $$$$ and it can add up quicly depending on the size of the service.
* It can add load to the cluster as it needs new relic infrastructure to send logs, potentially creating bottle necks.
* Interface can get a little tricky because of huge amount of options.

### Google Cloud Stackdriver - https://cloud.google.com/stackdriver/docs

Google Cloud Operation , formerly Stackdriver's, focus in improving the performance and availability of large, complex applications running in the public cloud. It provides metrics detailing every layer of the 'stack' in the form of charts and graphs. 

It also supports multi-cloud environments, which is an advantage for our project, and provides a single information panel into users' cloud services. It provides views into the logs that are generated, and allows users to generate metrics from those logs as well as allowing users to receive alerts when metrics breach normal levels.

**PROS**

* Already within the GCP stack.
* Integrates with GKE and Prometheus.
* Log alerts can be set for any string which occurred in logs and get alerts on mail, slack.
* Ease creation of metrics to understand performance.
* Good documentation on integration APIs

**CONS**

* Cost $$$$ but it includes all product features for free. Only paying for storage.
* Default logs are available only for 30 days.
* Can be slow for searching and filtering the logs.

### DataDog - https://www.datadoghq.com/

Datadog is monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a data analytics platform.

It gives you deep visibility into Kubernetes clusters, with minimal setup. You can deploy the Datadog Agent on every node in your cluster using the DaemonSet or Datadog Operator to start collecting metrics.

**PROS**

* Quick configuration to start using the platform.
* More than 400 integrations [see here](https://docs.datadoghq.com/integrations/)
* Excells in troubleshouting complex systems. Can identify bugs with pinpoint accuracy. 

**CONS**

* Cost $$$$.
* Lasks deeper application-level insight that New Relic offers.


### Opsgenie - https://www.atlassian.com/software/opsgenie

OpsGenie provides alert and notification management as a service including on-call scheduling and escalation capabilities. It has a simple and flexible mail integration as well as a RESTful API allows almost every tool to integrate with it.

**PROS**

* Their alarm and notification system.
* Integration with other tools.

**CONS**

* Cost $$$$
* Not the best option for monitoring metrics, but rather for alarms and notifications.

## Analysis and Recommendation

Based on the facts presented above, what I learn gathering them and the specific requirements for our use case, I will now summarize them and suggest what I believe are the strongest candidates.

One thing I'd like to mention before starting is that probably the services analyze in this report, are within the strongest in the monitoring sector. All of them have great use cases, but we need to find the best for our one. Also, cost, eventhough it wasn't specifically address in the requirements, has played an important role in the final decision. 

In the self-hosted sector, tools like Zabbix or Icinga are great for monitoring, they have a good integration API, both can work with the services that we need to, there are good reviews about them being strong and reliable but, it seems that they are not the best suited to monitor Kubernetes clusters.

In my opinion, this is one of the key points. Monitoring a monolithic infrastructure is not the same as monitoring a microservice one. The chanllenges are different. So the recommended tool will have to work well with microservices and in particullary Kubernetes.


