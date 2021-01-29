# Monitoring System Options

A Report Evaluating the Best System Monitoring Tool/s For a K8s Platform on GCP

### Icinga

Icinga is not as well established as some of the other monitoring tools in this report. Icinga is a free product but the integration maybe costly (hrs).
Nodes can be congifigured as active or passive and this will allow for splitting load monitoring and database interactions (good for load balancing).

Pricing - 
Reliability -
Support - None
Features - Monotoring, Alerts (details affect services when there is downtime), Web Interface

How well does •Icinga• intergrate with K8s running in GCP?
How well does •Icinga• intergrate with GCP APIs?
How well does •Icinga• intergrate with Postgres, Redis, RabbitMG and MongoDB?

### Nagios

// Note there is Nagios-Cfore and Nagios-XI//

Nagios is very established and has a very big commuinity, supports more applications and langauges compared to Icinga
Pricing - 
Reliability - Very Reliable 
Support - Availvable
Features - 

How well does •Icinga• intergrate with K8s running in GCP?
How well does •Icinga• intergrate with GCP APIs?
How well does •Icinga• intergrate with Postgres, Redis, RabbitMG and MongoDB?



### Prometheus

Prometheus is the go to K8s monitoring tool, it is the only tool of its kind mentioned on the K8s monitoring tools page [1] (https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/). Prometheus is a member of the Cloud Native Computing Foundation

Pricing - 
Reliability -
Support - None
Features - Monotoring, Alerts (details affect services when there is downtime), Web Interface

How well does •Prometheus• intergrate with K8s running in GCP?
How well does •Prometheus• intergrate with GCP APIs?
How well does •Prometheus• intergrate with Postgres, Redis, RabbitMG and MongoDB?
-Running Prometheus is easily achieved the [prometheus-operator](https://github.com/prometheus-operator/prometheus-operator)
-Prometheus has exporters for intergrate with Postgres, Redis, RabbitMG and MongoDB.
