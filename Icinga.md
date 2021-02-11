### Icinga   

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
