# Monitoring tools report for Feeld

This document is an evaluation of the different solutions available in the market to monitor our Kubernetes cluster.

Kubernetes allows for better development experience, but the number of containers created and destroyed, the number of nodes, pods, services deployed within a cluster and the communication between these services, it adds complexity into the monitoring system. 

This explosion of metrics will have to be addressed by the recommended tool in a way that it makes it easier for engineers to manage and understand what is going on in the system as well as helping in the troubleshooting process.

The main goal of our monitoring system will be to enable us to make rational decisions based in data, to respond to incidents and to align the service with our business objectives. 

## Self-Hosted or SaaS?

Depending on the requirements of the project one can choose between self-hosted and SaaS monitoring solutions. 

The main difference between them is cost. Self-hosted solutions are usually open source, but that doesn't mean they are free, they come at a cost. Not only the cost of hosting them, but as well the cost of time one has to invest in set-ups in an ongoing basis, especially when such set ups are made up of multiple tools. 

SaaS solutions, in the other hand, usually offer an array of built-in features that help engineers get the data they need without the overhead of configuration. That doesn't mean they don't need to be configured, but probably the time spent in those configurations are less than in a self-hosted one. Of course, they cost money, but depending on the situation, they can be useful if the team wants to get up and running with monitoring but doesn't have much spare capacity for setting them up.

## Requirements

For this project, there are specific requirements for the solutions to integrate with other services: Postgres, Redis, RabbitMQ and MongoDB. As well as the strength, easiness, and reliability to integrate with Kubernetes and GCP.  

These requirements will have a great influence in the selection of the recommended solution.

Another factors like budget allocated to the project or the size of the actual cluster to monitor were excluded from the requirements I believe they play a part as well in the final decision so they will be included in the analysis. 

## Self-Hosted Solutions

### Icinga - https://icinga.com/

Icinga is a monitoring system which checks the availability of your network resources, notifies users of outages, and generates performance data for reporting.

Scalable and extensible, Icinga can monitor large, complex environments across multiple locations.

It has a plugin to connect it to Kubernetes but doesn't seem it’s used much. There seems to be another connector as well, but the ecosystem is not extensive developed.

**PROS**

* Provides data and alerts for availability, connectivity, and general health checks of your infrastructure.
* It's fast. Quick notifications on system issues thanks to its multithreaded design.
* Uses very similar plugins and add-ons to Nagios.
* 3rd party integrations with MongoDB, Redis, RabbitMQ (Nagios) and Postgres 

**CONS**

* Might need another tool to monitor Kubernetes cluster.
* Although it has a focus in community, there is not a huge amount of info available on how to configure it.  
* Mainly used for static infrastructure.


### Zabbix - https://www.zabbix.com/

Zabbix is designed to monitor a large number of network parameters and the health of servers, offering many data visualization and reporting features based on the stored data. 

Both large and small organizations can use Zabbix to monitor IT infrastructure. It provides monitoring metrics, among others network utilization, CPU load and disk space consumption.

It's capable of storing the data in an array of services. Visualization features are available as well as very flexible ways of analysing the data and alerting.

**PROS**

* High performance and capability. Able to monitor +100.000 devices.
* Enables you to scan the network for external services and take pre-defined actions upon discovery.
* Strong API integrations which makes it easy to extend.
* Real-time visualization and nice graphs

**CONS**

* Does not integrate easily with Kubernetes.
* Support sold separately.
* It can get difficult to configure.
* Not detailed documentation. Difficult for first timers. 

### Prometheus - https://prometheus.io/

Prometheus is an open-source monitoring and alerting toolkit initially built at Soundcloud. In 2016, joined the Cloud Native Computing Foundation as the second hosted project, after Kubernetes.

Works in a pull-based system. It sends a scrape request based on the configuration defined in the deployment file. The response to this scrape request is stored and parsed in storage along with the metrics for the scrape itself. This scraping endpoint allow metrics to be pulled from several Prometheus instances and store it in a custom database on the Prometheus server that can handle a massive influx of data. 


In addition, pulling it's a better way of identifying the health of the service because if the endpoint is not available it's pretty clear the service is not healthy, but if the service doesn’t push notifications the reasons might vary and is not as clear its health status. 

Sometimes, the pull endpoint it's unable to monitor if the container life span is short. For that, Prometheus uses a push gateway notification

**PROS**

* Reliable stand alone and self-contain. It works even if part of the infrastructure is down.
* No extensive set up needed, great community support, low complexity.
* Monitor of Kubernetes cluster node resources out of the box.
* Components available as docker images. Can be easily deployed in container environment
* Integrates with Postgres, Redis, RabbitMQ and MongoDB as well as other [tools](https://Prometheus.io/docs/instrumenting/exporters/)

**CONS**

* Difficult to scale. Might need several Prometheus servers to collect all the metrics if the applications grow after a certain threshold.
* Step learning curve into how to correctly configure it. As learning promQL, the query language needed to query database of metrics to end up creating Grifana dashboards
* Memory intensive. Can use fair amount of the memory when deployed within the cluster.
* Own graphical interface is lacking. Need to integrate it with dashboard platform like Grifana.

### Others

Other tools that were taking into account for this Self-Hosted list were Grafana, cAdvisor and FluentD. All of them are related to Prometheus in one way or another. 
cAdvisor, developed by Google, is a tool to analyse mainly individual containers, so it's missing the monitoring capabilities that we need on pods, nodes and other Kubernetes features.
Grafana expands the graphic capabilities of Prometheus and usually is used in conjunction with it. It can read promQL, the query language Prometheus uses to send data.
Systemd can also integrate with Prometheus monitoring. 

## SaaS

### New Relic - https://newrelic.com/

New Relic is a web application performance service designed to work in real-time with your live web app. New Relic Infrastructure provides flexible, dynamic server monitoring.

In addition to providing visibility into operational data it could also see the relationships between objects in a cluster using Kubernetes’ built-in labelling system.

It integrates with GKE and it has a multi-dimensional representation of a Kubernetes cluster from which you can explore your namespaces, deployments, nodes, pods, containers, and applications.

**PROS**

* Able to see the dashboard (Kubernetes cluster explorer) with the Kubernetes integration. 
* Automatically deployed agent to pods and access to Kubernetes events.
* Troubleshoot without the need of switching tools.
* Integrates with Postgres, Redis, RabbitMQ and MongoDB as well as other [tools](https://newrelic.com/integrations).
* Real time reports.

**CONS**

* Cost $$$$ and it can add up quickly depending on the size of the service.
* It can add load to the cluster as it needs new relic infrastructure to send logs, potentially creating bottle necks.
* Interface can get a little tricky because of huge number of options.

### Google Cloud Stackdriver - https://cloud.google.com/stackdriver/docs

Google Cloud Operation, formerly Stackdriver's, focus in improving the performance and availability of large, complex applications running in the public cloud. It provides metrics detailing every layer of the 'stack' in the form of charts and graphs. 

It also supports multi-cloud environments, which is an advantage for our project, and provides a single information panel into users' cloud services. It provides views into the logs that are generated and allows users to generate metrics from those logs as well as allowing users to receive alerts when metrics breach normal levels.

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

![datadog-logo](https://global-uploads.webflow.com/5defb8273d0a4ce99a0af8ee/5e326c0ea21b61e649e25812_Datadog.jpg)

<img src="https://global-uploads.webflow.com/5defb8273d0a4ce99a0af8ee/5e326c0ea21b61e649e25812_Datadog.jpg" width="100">

Datadog is monitoring service for cloud-scale applications, providing monitoring of servers, databases, tools, and services, through a data analytics platform.

It gives you deep visibility into Kubernetes clusters, with minimal setup. You can deploy the Datadog Agent on every node in your cluster using the DaemonSet or Datadog Operator to start collecting metrics.

**PROS**

* Minimal configuration to start using the platform.
* More than 400 integrations [see here](https://docs.datadoghq.com/integrations/)
* Excels in troubleshooting complex systems. Can identify bugs with pinpoint accuracy. 

**CONS**

* Cost $$$$.
* Lacks deeper application-level insight that New Relic offers.


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

One thing I'd like to mention before starting is that probably the services analyse in this report, are within the strongest in the monitoring sector. All of them have great use cases, but we need to find the best for our one. Also, cost, even though it wasn't specifically address in the requirements, has played an important role in the final decision. 

In the self-hosted sector, tools like Zabbix or Icinga are great for monitoring, they have a good integration API, both can work with the services that we need to, there are good reviews about them being strong and reliable but, it seems that they are not the best suited to monitor Kubernetes clusters.

In my opinion, this is one of the key points. Monitoring a monolithic infrastructure is not the same as monitoring a microservice one. The challenges are different. So, the recommended tool will have to work well with microservices and in particularly Kubernetes.

In the SaaS space, looks like all the tools analysed integrates well with Kubernetes. New Relic and Datadog, possibly among the most well-known brands, have Kubernetes monitoring as one of their selling points. Stackdriver, being part of the Google ecosystem can integrate with Kubernetes and SKE quite easily as well. 

Another feature of SaaS product is they are, generally, easier to configure than a self-hosted one. Of course, this ease comes with a price tag. Some of them also provide support for installation and configuration. Bringing to the table another argument that wasn't specify in the requirements but, I believe, it has weight in the final decision. The capacity and expertise of the team to implement the chosen tool. 

From the top 3 services analyse, Stackdriver is the most economic, and given that we are using GCP (although it also integrates with AWS), it would seem like a good option. New Relic and Datadog are a bit more expensive but they offer more features. New Relic's Kubernetes Cluster Explorer seems like a good way of identifying how the cluster is behaving in real time. Datadog dashboard looks good as well and, their system, apparently, can help us identify bugs with pinpoint accuracy, which is great for debugging. 

The last tool I want to mention in this analysis is Prometheus. Open source, part of the CNCF, consider for many as "de facto approach for monitoring Kubernetes", it has great and supportive community behind it, loads of tutorials online on how to configure it, it's reliable, stable, can integrate with a great number of services, like all of the SaaS services we discussed above so they could work in conjunction, it uses a pull approach of collecting metrics, which is consider a more reliable way that pushing metrics, it can get up and running quickly, it can keep working when part of the system is down... And the list goes on.

Of course, not everything about it is good about it. It can get difficult to scale if the infrastructure gets too big, there is a steep learning curve to configure it exactly as we wish, it can use a lot of cluster memory if deployed within it, the graphical interface is lacking functionality and so on, but the upsides overtake the downsides.

To conclude, after taken into consideration all of the above, the analysis of the different tools, their pros and cons, I believe the best tool for our use case it's Prometheus. Not only is open source, but the support from the community and its active users can help us set get it up and running. I was able to do it following instructions in a git repo, not that I believe it would be as easy in a real-world project but still. 

In addition, most of the items in the list of downsides can be fixed, like the graphical interface with Grafana or the scaling of the service by dividing it into several servers. Maybe it's a bit complicated at the beginning but I'm up for the challenge.

In the microservice world, we need monitoring systems that allow us to alert for high-level services objectives but retain the granularity to inspect individual components as needed and I believe Prometheus is the one that can achieve this better for us.
