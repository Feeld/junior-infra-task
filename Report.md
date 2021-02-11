
# Introduction

This is my report detailing my evaluation and findings for a monitoring system looking at self-hosted and SaaS (Software-as-a-Service)options.

Feeld's platform is built around using Kubernetes (PaaS/ SaaS/ IaaS) on Google Cloud Platform (SaaS) and this evaluation will consider several systems/ service's that would need to integrate with these and Google Cloud Platform APIs aswell as Feeld's other existing systems Postgres, Redis, RabbitMQ and MongoDB.

As part of of this I will be contrasting and comparing:

* Icinga
* Zabbix
* Prometheus
* New Relic
* Google Cloud Stackdriver
* OpsGenie

Things I will be taking into consideration will be ease of use, strengths, maintainability, weaknesses's, cost, realiability and genrally looking into the option as being fit for the buisnnes's purpose.

# Icinga   

Icinga is a free open-source network tool used by the likes of Adobe, Audi, T mobile and Siemens that claims to be flexible, efficient, scalable and provides automated monitoring of a business’s network resources. 

It checks these and generates notifications of outages, surges and general performance metrics visually via dashboards with the ability to be filtered for reporting and monitoring purposes. Scalable and with the ability to stretch indefinitely, Icinga can monitor large, complex environments across multiple locations.

Incing’s RESTful API allows integration with Google Cloud Platform via HashiCorp Terraform, one of the tools made available in the Advanced Nagios Plugins Collection. This allows Icinga integration with Redis, RabbitMQ, Postgres, MongoDB and Kubernetes. 

### Pro’s

* Can send notifications in a variety of different (possible more helpful) ways, (Text message and Slack being two of my favourite methods)
* Scores highly (9.9 out of 10) on https://www.trustradius.com/
* Easy to read dashboard
* Easily scalable
* Flexible (monitoring is done by scripts so as long as you can write it, you can monitor it)
* Configuration is based on common props
* Large community support and plugin library
* Supports distributed monitoring
* Does what we require (integrates with Redis, RabbitMQ, Postgres, MongoDB and Kubernetes

### Con’s

* Configuration can be confusing and difficult to set up and deploy
* Difficult to integrate into modern management systems , no native support as such
* Maybe relies too much on third party plugins
* Is a fork of Nagios and therefore some feel, too outdated
* No simple way to add new hosts and services through the web UI, unmodern
* Inability to copy and paste has been reported therefore wasting time retyping

# Zabbix

Zabbix is a free open source software tool that combines a real-time monitoring of IT components and services, such as networks, servers, VMs, applications and the cloud with a breadth of 22 years’ experience and is used by companies such as T-Mobile, BodyBuilding.com, Dell and BookingLive.

It provides the user with monitoring metrics and logs, such as network utilization, CPU load and disk space consumption and displays them within a graphical user interface (GUI) that contains fully customisable dashboards based on widgets, graphs, network maps, slideshows and reports.
Zabbix also uses a flexible notification mechanism that allows users to configure e-mail-based alerts.

Zabbix utilises a web-based API that helps users to create new applications, automate tasks and integrate with third-party software.

Although not being native it does integrate with Kubernetes using 3 different solutions; a Docker Template, a Nagios/Icinga/Zabbix style plugin for checking Kubernetes and a option to provide a custom database container. There is also integration with Google Cloud Platform using its Stackdriver monitoring service as well as Redis, RabbitMQ and Postgres monitoring are all supported by Zabbix via templates while MongoDB requires one of several third-party template plugins.

### Pro’s
* Collects metrics from a variety of sources
* Uses a variety of different methods to alert users of issues
* Strong encryption between all Zabbix components
* Flexible dashboard which can be configured according to the need of the user
* Comes with lots of preconfigured templates for service profiles and servers
* Web based API that’s easy to use
* Good community support and there are many youtube videos which assist step by step installation

### Con’s
* Notification logic can be tricky to navigate and spam users
* Documentation can be scarce
* Hard for newbies to configure, support tickets and courses can be expensive
* Version migration could have been smoother in the past
* Doesn't support all file format’s

* **Requirements** https://github.com/AmyLouise85/junior-infra-task/blob/main/Requirements.md
* **A list of websites used in compiling this report can be found at** https://github.com/AmyLouise85/junior-infra-task/blob/main/Research.md
