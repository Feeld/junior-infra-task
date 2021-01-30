# Monitoring System Options

A Report Evaluating the Best System Monitoring Tool/s For a K8s Platform on GCP

Monitoring the cluster gives an acrros the board/overall platform health view, cluster resource utilisation (is infrastructure under- or over-utalised).

### Icinga

Icinga is not as well established as some of the other monitoring tools in this report. Icinga is a free product but the integration maybe costly (hrs).
Nodes can be congfigured as active or passive and this will allow for splitting load monitoring and database interactions (good for load balancing).

Pricing - \
Reliability - \
Support - None \
Features - Monotoring, Alerts (details affect services when there is downtime), Web Interface 

How well does *Icinga* intergrate with K8s running in GCP? \
How well does *Icinga* intergrate with GCP APIs? \
How well does *Icinga* intergrate with Postgres, Redis, RabbitMG and MongoDB? 

### Nagios

// Note there is Nagios-Core and Nagios-XI//

Nagios is an established and has a very big commuinity, supports more applications and langauges compared to Icinga. It is generally considered to be a greate monitoring tool for static infrastructure (it would be easier to monitor host device and trickier to monitor containers). 

Github - 33 forks, ~5 contributors
Pricing - 
Reliability - Very Reliable 
Support - Availvable
Features - 

How well does *Nagios* intergrate with K8s running in GCP?
How well does *Nagios* intergrate with GCP APIs?

There is a [service](https://console.cloud.google.com/marketplace/product/cloud-infrastructure-services/nagios-ubuntu-20-04?pli=1&project=autobot-296021&folder=&organizationId=) for Nagios Core monitoring setup on GCP with a Cost of ~£35.00. Another option is to use [check_rest_api](https://exchange.nagios.org/directory/Plugins/Network-Protocols/HTTP/check_rest_api-%7C-Monitor-data-from-a-REST-API/details), a plugin used to monitor data from REST APIs.

How well does *Nagios* intergrate with Postgres, Redis, RabbitMG and MongoDB?

Most Nagios plugins, addons or extensions can be dound on the [exchange](https://exchange.nagios.org). Another noteworthy project is the [Advanced Nadios Plugin Collection](https://github.com/harisekhon/nagios-plugins).

- Nagios can be used to monitor Redis with a list of the plugins that can be found [here](https://github.com/harisekhon/nagios-plugins). There is also a [Regis Enterprise Software Nagios Plugin](https://docs.redislabs.com/latest/rs/administering/monitoring-metrics/nagios-plugin/).
- There are [MongoDB plugins](https://github.com/mzupan/nagios-plugin-mongodb) that can be used to monnitor MongoDB wiith Nadios.
- Nagios can be used to monitor Redis using a list of the plugins that can be found [here](https://github.com/harisekhon/nagios-plugins)
- [Nagios](https://www.nagios.com/solutions/postgres-monitoring/) offers Postgres monitoring, including connection status, databases, table sizes and other metrics.


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

## Conclusion

Icinga and Nagios have the necessary features and addons/extension to make them useful for Kubeneters monitoring. These tools are developed and mantained by very small communities and this is not are bad thing but it does indicate the level of interest in these tools on the Kubernetes community. More popular projects usually mean more contributors and that can translate to meore people who understand the code theus, when there are issues the are more people to help with troubleshooting and chances are that someone in the community would have had the same issue at some point.

Kubenetes components export metrics in Prometheus format

Pulling instead of pushing


