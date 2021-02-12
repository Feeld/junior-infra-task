
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

Icinga is a self-hosted, free open-source network tool used by the likes of Adobe, Audi, T mobile and Siemens that claims to be flexible, efficient, scalable and provides automated monitoring of a business’s network resources. 

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

Zabbix is a self-hosted, free open source software tool that combines a real-time monitoring of IT components and services, such as networks, servers, VMs, applications and the cloud with a breadth of 22 years’ experience and is used by companies such as T-Mobile, BodyBuilding.com, Dell and BookingLive.

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
* Scores pretty low (7.7 out of 10) on https://www.trustradius.com/

# Prometheus 

Prometheus is a self-hosted, free open-source monitoring software that utilises autonomous single server nodes, trusted by Boxever, Docker, KuberMatic and SoundCloud.

Looks to have exceptional native integration with its Cloud Native Computing Foundation partner Kubernetes as it appears to be the only software actively championed by them. It can also be easily integrated with Google Cloud Platform but Redis, RabbitMQ Postgres and MongoDB need to be monitored with third parties.

Prometheus relies on scraping metrics from predefined exposed endpoints that happen via a pull model over HTTP that instruct the server how to scrape it. Although not having. huge native DB, there are third party exporters available for many applications that have an easy way to add web endpoints, such as Kafka and Cassandra.  

Each Prometheus server is standalone, not depending on network storage or other remote services claiming you can rely on it when other parts of the infrastructure are broken, and no extensive setup infrastructure is needed to use it.

### Pros

* has a very active developer and user community
* multiple modes of graphing and dashboarding support
* supports over 10 dev languages
* precise alerting
* scores highly (9 out of 10) at https://www.trustradius.com

### Cons

* collected data will likely not be detailed and complete enough for 100% accuracy
* official support has been reported as lacking
* only alerts on critical responses such as production issues, incident response, post- mortem analysis, and metrics (good tho?)

# New Relic

New Relic One is a chargeable, SaaS, cloud based, web and mobile observability platform that claims to help businesses analyse, troubleshoot, and optimize an entire software stack in real time.

Claims to help increase flexibility and speed with their open platform and commitment to open-source standards and gives the user the ability to create custom observability apps for full customisation. 

Trusted by companies such as MasterCard and Spotify it integrates natively with the Google Cloud Platform services, including the Google Kubernetes Engine, Redis, MongoDB, RabbitMQ and Postgres.

### Pros
* Unified AI UI
* Natively integrates with our stack
* Works across web and mobile
* Works across Cloud and Hybrid environments
* Scored highly (8.1 out of 10) on https://www.trustradius.com/
* Benefits from strong community support

### Cons
* Only free up to a certain point, could get costly and would need further BA input

# Google Cloud Stackdriver

I Don’t think Google really needs much introduction (!) but it’s safe to say this SaaS cloud management system is used and trusted by some of the biggest companies in the world. Stackdriver is free up to a certain point and claims to be designed to keep apps running fast, error free and available in the Cloud.

Monitors and alerts metrics from GCP such as Cloud logging, error reporting, trace and production debugger, diagnostic and performance data and displays them in graphs and charts for ease of use. 

Nativity integrates with other member of the ‘Google family’ such as Google Kubernetes Engine but integration with Postgres, MongoDB or Rabbit MQ doesn’t look like it has much support and is almost advised against instead using BlueMedora to BindPlane our stack to Stackdriver.

Boasts a world-class reliability and scalability as the service is migrated to the same infrastructure that powers the rest of Google.

### Pros
* Uses Slack for notifications
* Brandname
* Huge community support and excellent documentation/ you tube

### Cons
* Cost
* Intergration with our stack

# OpsGenie

Opsgenie is a chargeable, SaaS, real time incident management solution, powered by Atlassian. It receives alerts from our separate monitoring systems and custom applications (acting as a single source of truth) and categorises each alert based on importance and timing and alerts a designated or specific person/s.

Multiple communication channels including voice calls, email, SMS, and push messages on mobile devices. If an alert is not acknowledged or seen by its assignee, Opsgenie automatically escalates it, ensuring the incident gets the attention needed :)

Looks to integrate with Stackdriver and MongoDB but relies on a variety of paid/ freemium third parties for the rest of our stack  

### Pros
* Community support on social media
* Uses a variety of methods to contact user including Slack and voice calls
* Has a app on the PlayStore
* Scores highly (9.2 out of 10) on www.trustradius.com
* Easy to use GUI
### Cons
* Doesn’t *actually* monitor applications or systems is more of an alert only system albeit a good one.
* Only integrates with half our stack
* Cost- outweighs for what it actually provides


* **Requirements** https://github.com/AmyLouise85/junior-infra-task/blob/main/Requirements.md
* **A list of websites used in compiling this report can be found at** https://github.com/AmyLouise85/junior-infra-task/blob/main/Research.md
