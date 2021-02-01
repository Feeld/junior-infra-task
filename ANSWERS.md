# Monitoring System Options

A Report Evaluating the Best System Monitoring Tool/s For a K8s Platform on GCP

Monitoring the cluster gives an acrros the board/overall platform health view, cluster resource utilisation (is infrastructure under- or over-utalised).

## Table of contents
1. [Icinga](#icinga)
2. [Zabbix](#zabbix)

<a name="icinga"/>

#### Icinga

Github - 480 forks, ~240 contributors

Icinga is a free product but the integration maybe costly (hrs).
Nodes can be congfigured as active or passive and this will allow for splitting load monitoring and database interactions (good for load balancing).

Ease:

  Icinga is not easy to intergrate with kubernetes, there is no native support for monitoring kubernetes clusters with Icinga but there are tools available mantained by the Icinga community. [Check_Kubernetes](https://exchange.icinga.com/neubi4/check_kubernetes) is a plugin that can be found on the Icinga exchange, it provide deployment, nodes, scheduler, and controller information. For Cloud services and or Kubernetes, target the load balancer address or the Kubernetes Service or Ingress addresses for monitoring.
    GCP ApIs - No specialised gcp support but there some are tools made available in the [Advanced Nagios Plugins Collection](https://exchange.icinga.com/harisekhon/Advanced%20Nagios%20Plugins%20Collection%20%28NoSQL%2C%20Hadoop%2C%20Redis%2C%20Cassandra%2C%20Elasticsearch%2C%20Solr%2C%20MySQL%2C%20Linux%2C%20HBase%2C%20MongoDB%20etc%29), they allow Icinga integration with Redis, RabbitMQ, Postgres and MongoDB. The documentatioin [here](https://exchange.icinga.com/harisekhon/Advanced%20Nagios%20Plugins%20Collection%20%28NoSQL%2C%20Hadoop%2C%20Redis%2C%20Cassandra%2C%20Elasticsearch%2C%20Solr%2C%20MySQL%2C%20Linux%2C%20HBase%2C%20MongoDB%20etc%29) suggests that these plugins can allow extensive checks.

Features: 

  Monotoring (Performance), Alerts, Text Notifications, Dashboards (visualisation), REST API, 

Reliability:

  Icinga does not offer kubernetes native support, the integration is through Nagios plugins which are mantained by the community. The kubernetes-nagios communities are signficantly smaller than some of the other kubernetes monitoring projects. Thus, I would *rely* on the projects with more support and with features that align with this project.

<a name="zabbix"/>

### Zabbix

Github - ~444 forks, ~8 contributors

Ease:

  K8s - Not possible out of the box but some [solutions](https://www.zabbix.com/integrations/kubernetes) are available, using docker images and Nagios like [extensions](https://github.com/agapoff/check_kubernetes).
  GCP APIs - Zabbix can be intergrated for GCP monitoring using the Stack Driver API, instructions available [here](https://github.com/ingrammicro/gcpmetrics/wiki/Google-Cloud-Platform-monitoring-with-Zabbix).
  Postgres - A Zabbix [template](https://www.zabbix.com/integrations/postgresql) is available for Postgres monitoring.
  Redis - There is an out of the box Zabbix [template](https://www.zabbix.com/integrations/redis) for Redis monitoring.
  RabbitMQ - Out of the box RabbitMQ intergration using a [template app](https://www.zabbix.com/integrations/rabbitmq).
  MongoDB - There are several Zabbix [plugins](https://www.zabbix.com/integrations/mongodb) available for monitoring MongoDB.
  
Features:

  K8s - The [check_kubernetes](https://github.com/agapoff/check_kubernetes) extension will allow for checking failed jobs, TLS certificates, deployments,apiserver health and a few more metrics.
  GCP APIs - GCP metrics of monitored recourses if integrated with Stack Driver API.
  Postgres - Monitors Tablespaces, Databases, Namespaces, Tables and Indexes.
  Redis - Availability, Memory and Databases
  RabbitMQ - Will Monitor Channels, Exchanges, Ques.
  MongoDB -  Availability, resource utilization and health.

Reliability:

Zabbix maybe reliable for the systems it offers native monitoring solutions for (Zabbix has out of the box intergration soultions for half of the systems in the stack.)  but it is hard to say for the non-native supported system.

<a name="nagios"/>

### Nagios

Github - 33 forks, ~5 contributors

Nagios is an established and has a very big commuinity, supports more applications and langauges compared to Icinga. It is generally considered to be a greate monitoring tool for static infrastructure (it would be easier to monitor host device and trickier to monitor containers).

Ease:

The google cloud [documentation](https://cloud.google.com/docs/compare/data-centers/management) mentions 
There is a [service](https://console.cloud.google.com/marketplace/product/cloud-infrastructure-services/nagios-ubuntu-20-04?pli=1&project=autobot-296021&folder=&organizationId=) for Nagios Core monitoring setup on GCP with a Cost of ~£35.00. Another option is to use [check_rest_api](https://exchange.nagios.org/directory/Plugins/Network-Protocols/HTTP/check_rest_api-%7C-Monitor-data-from-a-REST-API/details), a plugin used to monitor data from REST APIs. The [Advanced Nagios Plugins Collection](https://exchange.icinga.com/harisekhon/Advanced%20Nagios%20Plugins%20Collection%20%28NoSQL%2C%20Hadoop%2C%20Redis%2C%20Cassandra%2C%20Elasticsearch%2C%20Solr%2C%20MySQL%2C%20Linux%2C%20HBase%2C%20MongoDB%20etc%29) makes available tools for Kubernetes, MongoDB, Postgres, RabbitMQ and Redis. 
Most Nagios plugins, addons or extensions can be dound on the [exchange](https://exchange.nagios.org). Another noteworthy project is the [Advanced Nadios Plugin Collection](https://github.com/harisekhon/nagios-plugins).

- Nagios can be used to monitor Redis with a list of the plugins that can be found [here](https://github.com/harisekhon/nagios-plugins). There is also a [Regis Enterprise Software Nagios Plugin](https://docs.redislabs.com/latest/rs/administering/monitoring-metrics/nagios-plugin/).
- There are [MongoDB plugins](https://github.com/mzupan/nagios-plugin-mongodb) that can be used to monnitor MongoDB wiith Nadios.
- Nagios can be used to monitor Redis using a list of the plugins that can be found [here](https://github.com/harisekhon/nagios-plugins)
- [Nagios](https://www.nagios.com/solutions/postgres-monitoring/) offers Postgres monitoring, including connection status, databases, table sizes and other metrics.

Features:
  
  Monitoring, Web Interface, Notifications, Event Handlers (proactive problem resolution) and Log File Archiving.

Reliability:

<a name="prometheus"/>

### Prometheus

Ease:

How to integrate Prometheus monitoring to:
  K8s - GCP APIs - Postgres - Redis - RabbitMQ - MongoDB - 
  
Features:
  
  

Reliability:


### New Relic

All in one monitoring.
See performance from the end users point of view.

Ease:

How to integrate New Relic monitoring to:
  K8s - GCP APIs - Postgres - Redis - RabbitMQ - MongoDB - 
  
Features:
  


Reliability:

  Even if there was a move to heroku or AWS, New Relic supports both platforms

### Google Stack Driver

Ease:

How to integrate Google Stack Driver monitoring to:
  K8s - GCP APIs - Postgres - Redis - RabbitMQ - MongoDB - 
  
Features:
  


Reliability:



### Prometheus

Prometheus is the go to K8s monitoring tool, it is the only tool of its kind mentioned on the K8s monitoring tools [page](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/) and like kubernetes prometheus is also a member of the Cloud Native Computing Foundation (CNCF) project.

Github - 2,400 forks, ~400 contributors
Pricing - \
Reliability - \
Support - None \
Features - Monotoring, Alerts (details affect services when there is downtime), Web Interface \

How well does *Prometheus* intergrate with K8s running in GCP? \
How well does *Prometheus* intergrate with GCP APIs? \
How well does *Prometheus* intergrate with Postgres, Redis, RabbitMG and MongoDB? \

-Running Prometheus on K8s is easily achieved with the [prometheus-operator](https://github.com/prometheus-operator/prometheus-operator) \
-Prometheus has exporters for intergrate with Postgres, Redis, RabbitMG and MongoDB.

### Stack Driver 

Monitors the costs of GCP usage.

If there are a number o recourse being used Stack Driver can get expensive.

### OpsGenie

OpsGenie is a 

## Key Metrics
Key metrics for Kubernetes monitoring:
Key metrics for RabbitMQ monitoring:

## Conclusion


|             | Icinga                |Zabbix                 |Prometheus              |New Relic               |Google Cloud Stackdriver|Opsgenie             |
| ------------|:---------------------:|----------------------:|-----------------------:|:----------------------:|-----------------------:|--------------------:|
| Ease of Use | right-aligned | $1600 |                       |                        |                        |                        |                     |
| Features    | centered      |   $12 |                       |                        |                        |                        |                     |
| Reliability | are neat      |    $1 |                       |                        |                        |                        |                     |
| Reliability | are neat      |    $1 |                       |                        |                        |                        |                     |


Icinga and Nagios have the necessary features and addons/extension to make them useful for Kubeneters monitoring. These tools are developed and mantained by very small communities and this is not are bad thing but it does indicate the level of interest in these tools on the Kubernetes community. More popular projects usually mean more contributors and that can translate to meore people who understand the code theus, when there are issues the are more people to help with troubleshooting and chances are that someone in the community would have had the same issue at some point.

Monitoring the cluster gives an across an overall view of platform health,

Kubenetes components export metrics in Prometheus format

Pulling instead of pushing

When there is a problem with a tool that does not have a significant community it will require more time to find a solution. 

