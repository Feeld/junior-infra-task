# Monitoring System Options

A Report Evaluating the Best System Monitoring Tool/s For a Kubernetes Platform on GCP

Monitoring the cluster gives an across the board/overall platform health view, cluster resource utilisation (is infrastructure under- or over-utalised).

## Table of contents

1. [Self-Hosted Tools](#selfhosted)
    1. [Icinga](#icinga)
    2. [Zabbix](#zabbix)
    3. [Nagios](#nagios)
    4. [Prometheus](#prometheus)
    5. [Table 1](#table1)
2. [SaaS Tools](#saas)
    1. [New Relic](#newrelic)
    2. [Google Stack Driver](#stackdriver)
    3. [OpsGenie](#opsgenie)
    4. [Table 2](#table2)
3. [Conclusion](#conclusion)
4. [Key Metrics](#keymetrics)

<a name="selfhosted"/>

## Self-Hosted Tools

<a name="icinga"/>

#### Icinga

Icinga is an open source computer and network monitoring tools. It is a free product but the integration maybe costly (hrs). I was a Nagios fork originally, nodes to be congfigured as active or passive and this will allow for splitting load monitoring and database interactions (good for load balancing).

Integrations:

  Icinga is not easy to intergrate with kubernetes, there is no native support for monitoring kubernetes clusters with Icinga but there are tools available maintained by the Icinga community. [Check_Kubernetes](https://exchange.icinga.com/neubi4/check_kubernetes) is a plugin that can be found on the Icinga exchange, it provide deployment, nodes, scheduler, and controller information. For Cloud services and or Kubernetes, the load balancer address or the Kubernetes Service or Ingress addresses have to be targeted for monitoring.
    Google Cloud Platform (GCP) ApIs are also not natively supported but there are some tools made available in the [Advanced Nagios Plugins Collection](https://exchange.icinga.com/harisekhon/Advanced%20Nagios%20Plugins%20Collection%20%28NoSQL%2C%20Hadoop%2C%20Redis%2C%20Cassandra%2C%20Elasticsearch%2C%20Solr%2C%20MySQL%2C%20Linux%2C%20HBase%2C%20MongoDB%20etc%29), they allow Icinga integration with Redis, RabbitMQ, Postgres and MongoDB. The documentatioin [here](https://exchange.icinga.com/harisekhon/Advanced%20Nagios%20Plugins%20Collection%20%28NoSQL%2C%20Hadoop%2C%20Redis%2C%20Cassandra%2C%20Elasticsearch%2C%20Solr%2C%20MySQL%2C%20Linux%2C%20HBase%2C%20MongoDB%20etc%29) suggests that these plugins can allow for extensive checks.

Features: 

  Monotoring (Performance), Alerts, Text Notifications, Dashboards (visualisation), REST API, 

Reliability:

  Icinga does not offer kubernetes native support, the integration is through Nagios plugins which are mantained by the community. The kubernetes-nagios communities are signficantly smaller than some of the other kubernetes monitoring projects. Thus, I would *rely* on the projects with more support and with features that align with this projects' stack.

<a name="zabbix"/>

### Zabbix

Integrations:

  Zabbix does not support Kubenetes out of the box but some [solutions](https://www.zabbix.com/integrations/kubernetes) are available, using docker images and Nagios like [extensions](https://github.com/agapoff/check_kubernetes). Zabbix can be intergrated with GCP monitoring using the Stack Driver API, instructions available [here](https://github.com/ingrammicro/gcpmetrics/wiki/Google-Cloud-Platform-monitoring-with-Zabbix). A Zabbix [template](https://www.zabbix.com/integrations/postgresql) is available for Postgres monitoring. There is an out of the box Zabbix [template](https://www.zabbix.com/integrations/redis) for Redis monitoring. Out of the box RabbitMQ intergration using a [template app](https://www.zabbix.com/integrations/rabbitmq). There are several Zabbix [plugins](https://www.zabbix.com/integrations/mongodb) available for monitoring MongoDB.
  
Features:

  The [check_kubernetes](https://github.com/agapoff/check_kubernetes) extension will allow for checking failed jobs, TLS certificates, deployments,apiserver health and a few more metrics. GCP monitoring metrics are made available if integrated with Stack Driver API.
  Postgres - Monitors Tablespaces, Databases, Namespaces, Tables and Indexes. Redis checks include availability, memory and databases. For RabbitMQ, Zabbix can monitor channels, exchanges, queues and for MongoDB, availability, resource utilization and health.

Reliability:

Zabbix may be reliable for the systems it offers native monitoring solutions for (Zabbix has out of the box intergration soultions for half of the systems in the stack.)  but it is hard to say for the non-native supported systems.

<a name="nagios"/>

### Nagios

Nagios is an established systems monitoring tool and has a very big commuinity, supports more applications and langauges compared to Icinga. It is generally considered to be a greate monitoring tool for static infrastructure (it would be easier to monitor host device and trickier to monitor containers).

Integrations:

The google cloud [documentation](https://cloud.google.com/docs/compare/data-centers/management) mentions that there is a [service](https://console.cloud.google.com/marketplace/product/cloud-infrastructure-services/nagios-ubuntu-20-04?pli=1&project=autobot-296021&folder=&organizationId=) for Nagios Core monitoring setup on GCP with a Cost of ~£35.00. Another option is to use [check_rest_api](https://exchange.nagios.org/directory/Plugins/Network-Protocols/HTTP/check_rest_api-%7C-Monitor-data-from-a-REST-API/details), a plugin used to monitor data from REST APIs. The [Advanced Nagios Plugins Collection](https://exchange.icinga.com/harisekhon/Advanced%20Nagios%20Plugins%20Collection%20%28NoSQL%2C%20Hadoop%2C%20Redis%2C%20Cassandra%2C%20Elasticsearch%2C%20Solr%2C%20MySQL%2C%20Linux%2C%20HBase%2C%20MongoDB%20etc%29) makes available tools for Kubernetes, MongoDB, Postgres, RabbitMQ and Redis. 
Most Nagios plugins, addons or extensions can be found on the [exchange](https://exchange.nagios.org).

- Nagios can be used to monitor Redis with a list of the plugins that can be found [here](https://github.com/harisekhon/nagios-plugins). There is also a [Regis Enterprise Software Nagios Plugin](https://docs.redislabs.com/latest/rs/administering/monitoring-metrics/nagios-plugin/).
- There are [MongoDB plugins](https://github.com/mzupan/nagios-plugin-mongodb) that can be used to monnitor MongoDB wiith Nadios.
- Nagios can be used to monitor Redis using a list of the plugins that can be found [here](https://github.com/harisekhon/nagios-plugins)
- [Nagios](https://www.nagios.com/solutions/postgres-monitoring/) offers Postgres monitoring, including connection status, databases, table sizes and other metrics.

Features:
  
  Monitoring, Web Interface, Notifications, Event Handlers (proactive problem resolution) and Log File Archiving.

Reliability:

  It is said to run realibly once setup, especially for  static infrastructure. DHL, Domino's Pizza, McAfee all use Nagios but it is worth noting that they may be using an Enterprise verison of Nagios that comes with support.

<a name="prometheus"/>

### Prometheus

<a name="gitpop"/>

Prometheus is the go to Kubernetes monitoring tool, it is the only tool of its kind mentioned on the Kubernetes monitoring tools [page](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/) and like kubernetes, prometheus is also a member of the Cloud Native Computing Foundation (CNCF) project.

Integrations:

- Running Prometheus on Kubernetes is easily achieved with the [prometheus-operator](https://github.com/prometheus-operator/prometheus-operator) \
- RabbitMQ natively exposes Prometheus  [Metrics](https://rabbitmq.com/prometheus.html)
- Prometheus has exporters for intergratation with [Postgres](https://github.com/wrouesnel/postgres_exporter), [Redis](https://github.com/oliver006/redis_exporter), [RabbitMG](https://github.com/kbudde/rabbitmq_exporter) and [MongoDB](https://github.com/dcu/mongodb_exporter).
  
Features:

  Dimension Data Model, Querying Time Series Data, Grafana Intergration, Monotoring, Precise Alerting and Many Intergrations.
  
Reliability:
  
  The Prometheus [documentaion](https://prometheus.io/docs/introduction/overview/) details that "*Prometheus is designed for reliability*", additionally it states that prometheus can be relied on when other parts of your infrastructure is down. The reliance of organisations such as [Uber](https://www.uber.com/), [Slack](https://slack.com/) [Robinhood](https://robinhood.com/us/en/) and the popularity on [github](#table1) are indicators that Prometheus is a reliable monitoring tool.
  
<a name="table1"/>

|             | Icinga      |Zabbix       |Nagios        |Prometheus         |
| ------------|:-----------:|------------:|-------------:|------------------:|
| Forks       | 480         |440          |340           |5.6k               |
| Stars       | 1.5k        |1.4k         |919           |35.1k              |
| Contributors| 240         |8            |52            |560                |

**Table: 1** Showing github popularity for the open soure monitoring tools. Prometheus is the favoured tool.


<a name="saas"/>

## SaaS Tools

<a name="newrelic"/>

### New Relic

New Relic is described as an all in one, full stack perfomance monitoring system capable of producing metrics that can elucidate the users experience.

Integrations:
  
  New relic can be Integrated with Kubernetes using a manifest that is generated by an automated installer, this integration also works with [Google Kubernetes engine](https://docs.newrelic.com/docs/integrations/kubernetes-integration/installation/kubernetes-integration-install-configure). Postgres, Redis, RabbitMQ and MongoDB can also be monitored using the the [New Relic's on host integrations](https://docs.newrelic.com/docs/integrations/kubernetes-integration/link-apps-services/monitor-services-running-kubernetes#requirements).
  
Features:
  
  Monitoring (Response Time, Throughput, and Error Rates), Performance Data API, SQL Query Analysis, Alerting, Deployment Monitoring and Security.

Reliability:

  New Relics offer a realible service and they are trusted by over ~1700 customers including [Mastercard, Paytm and Spotify](https://stackshare.io/stackups/stackdriver-vs-icinga-vs-new-relic). Customer's data is stored in a Tier III, SSAE-16 certified centers and regulary backed up.
  The products they offer are tested. If one encounters issues there is [support](https://docs.newrelic.com/docs/licenses/license-information/general-usage-licenses/global-technical-support-offerings) available depending on subscruption level. In addition to the support service, there is a [community service](https://discuss.newrelic.com) and [open source projects](https://github.com/newrelic). 
  
<a name="stackdriver"/>

### Google Cloud Stackdriver

Google stack driver is now known as (Google Cloud's operations suite). It's a cloud compute management system offering applications and infrastructure, dignostic and perfomance data.

Integrations:
  
  Google Cloud's operations suite has out of the box integration with Kubenetes (part of the [monitored-resources](https://cloud.google.com/monitoring/api/resources)), GCP APIs including Google Kubernetes Engine (GKE) are monitored-resources. To monitor a resource that is not supported as a monitored-resource such as Postgres, RabbitMQ and MongoDB, Google Cloud's operations suite uses [bindplane](https://docs.bindplane.bluemedora.com/docs/bindplane-sources) for intergration. Cloud monitoring can still discover a Redis instance running on the the [Cloud Platform project](https://cloud.google.com/monitoring/agent/plugins/redis), if "redis" is in the names of **VM instances** and firewall rules open to **6379**.
  
Features:
  
  Monitoring, Logging, Alerting, Tracing, Production Debugger, Querying, Dashboards and Multi-Cloud (Supports AWS).

Reliability:

  Most Goodle services are reliable and the same can be said for Google Cloud's operations suite. It provides Cloud Logging which securely stores data and alerts on all log data and events, [Error reporting](https://cloud.google.com/error-reporting/docs/) which automatically analyzes logs for excpetions. It is also very useful for improving perfomance and data analysis.

<a name="opsgenie"/>

### OpsGenie

Integrations:

OpsGenie is a Cloud software services that offers alerting, on-call scheduling and incident management tools. Opsgenie intergrates with monitoring tools and services and helps with alerting, it does not offer any monitoring tools itself. 

Features:

  Alerting, On-Call Manegement and Operational Efficiency Analytics.

Reliability:

  It is very reliable for alerting because of the variety of alerting tools it has including [multiple-alerting-channels](https://www.atlassian.com/software/opsgenie/it-alerting#multiple-alerting-channels) and the ability to escalate alerts. If a team-member that is on-call is alerted through a text or a slack ping and they don't respond OspGenie can call them. If they do not pick-up, an escaltion is carried out depending on the configuration, a call can be made to the next person inline or the entire team is alerted. Opsgeneie also reduces noise from alerts by assigning priority.

<a name="table2"/>

|             | New Relic             |Google Stackdrive      |Opsgenie                |
| ------------|:---------------------:|----------------------:|-----------------------:|
| Stacks      |17.5k                  |275                    |171                     |
| Followers   |5.7K                   |275                    |161                     |
| Votes       |1.9K                   |65                     |23                      |

**Table: 2** Showing popularity based on [Stakeshare](https://stackshare.io/stackups/stackdriver-vs-new-relic-vs-opsgenie) for the SaaS monitoring tools. New relic is the popular tool in this category.


<a name="conclusion"/>

## Conclusion

Zabbix, Icinga and Nagios have the necessary features and addons/extensions to make them useful for Kubeneters monitoring. These tools were developed ealier than Prometheus but they are mantained by very small communities in comparison [see table 1](#table1). This is not are bad thing but it does indicate the level of interest in these tools in the Kubernetes community. More popular projects usually mean more contributors and that can translate to more people who understand the code thus, when there are issues, the are more people to help with troubleshooting and chances are that someone in the community would have had the same issue at some point.

Although New Relic can produce some interesting metrics driven by their data analysis processes, I believe the same data can be made available through prometheus using [PromQL](https://prometheus.io/docs/prometheus/latest/querying/basics/). Google Cloud's operations suite also offers similar data analytics driven solutions for perfomance and it also offers seemless integration with GCP APIs but RabbitMQ, MongoDB and Postgres require a [3rd part](https://docs.bindplane.bluemedora.com/docs/bindplane-sources) addon and the more resources you use the more you pay.

Due the reason I mentioned above, the cost, the ease of use and and the [popularity](table1), I select Prometheus as a monitoirng tool. Additonally, Kubernetes and Prometheus are both members of the CNCF. Kubenetes components export metrics in Prometheus format, there are exporters available for all the systems in the stack and Prometheus is not platform dependent. It pulls instead of pushing which allows for monitoring during development and I can inspect the metrics endpoint manually or with other tools. Overall Prometheus is open source, offers an extensive amount of significant features, native intergation with Kubernetes, can potentially be configured to acquire some of the metrics made avaivable in paid services and has a big enough community to help with troubleshooting.


<a name="keymetrics"/>

## Key Metrics to Monitor

Key metrics for **Kubernetes** monitoring:
  - Running Pods and Deployments
  - Resource Metrics (CPU, Memory and Disk I/O)
  - Container Native Metrics (Container Health)
  - Applications Metrics
  - Ready (Node ready for Pods)
  - MemoryPressure
  - DiskPressure
  - NetworkUnavailable

RabbitMQ, MongoDB and Postgres may also need infrastructure Monitoring (CPU, Memory, Disk I/O and Network Throughput...), only the application specific metrics are added below.

Key metrics for **RabbitMQ** monitoring:
  - Exchange perfomance
  - Connection
  - Queue Perfomance (Message publish/delivery rate)
  
Key metrics for **Redis** monitoring:
  - Client and connection Statistics
  - Persistence Statistics 
  - Operation Statistics
  - Keyspace Statistics
  - Replication Details
  - Expired Key Statistics
  
Key metrics for **MongoDB** monitoring:
  - Database Connections
  - Disk Utilization
  - Replica State 
  - Locking State
  
Key metrics for **Postgres** monitoring:
  - Responce Time
  - Active Sessions
  - Disk Usage
  - Locks
  - Transaction Details
  - Read Query Throughput
  - Write Query Throughput
  - Replication
