### Zabbix

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
