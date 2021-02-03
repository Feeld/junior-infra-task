Evaluate options for monitoring system.

- difference between self hosted and SaaS
- consider strength, ease reliability
- easiness to work with K8 and GCP
- postgres, redis, rabbitMQ, mongoDB

Self-hosted

    Icinga - https://exchange.icinga.com/itrsgroup/check_k8s
    Zabbix - https://www.zabbix.com/integrations/kubernetes
    Prometheus - 

SaaS

    New Relic 
    Google Cloud Stackdriver
    OpsGenie

mine

    riemann
    heka,
    bosun
    prometheus + sysdig 


----------------------------------------------------------

ideas to write document

 “We need monitoring systems that allow us to alert for high-level service objectives, but retain the granularity to inspect individual components as needed.” 
 
 
Monitoring enables service owners to make rational decisions about the impact of changes to the service, apply the scientific method to incident response, and of course ensure their reason for existence: to measure the service’s alignment with business goals



In recent years, monitoring has undergone a Cambrian Explosion: Riemann, Heka, Bosun, and Prometheus have emerged as open source tools that are very similar to Borgmon’s time-series–based alerting.

They allow the system overhead to be kept low so that the people running the services can remain agile and respond to continuous change in the system as it grows.

[font](https://sre.google/sre-book/practical-alerting/)



This is why monitoring tools that provide granular visibility through system calls tracing allow you to see down to every process, file or network connection that happened inside a container to troubleshoot issues faster. 


 Prometheus is the de facto approach for monitoring Kubernetes, and if you’re looking at implementing your own DIY Prometheus monitoring for Kubernetes, we wrote a guide on how to do it.

While it’s really easy to start monitoring Kubernetes with Prometheus, DevOps teams quickly realize that Prometheus has some roadblocks, like scale or RBAC, and teams support for compliance. You can read more about this on the Challenges using Prometheus at scale. 

 [font](https://sysdig.com/blog/monitoring-kubernetes/)


 It’s important to choose the adequate metrics and use as few as possible
 [font](k8 book)

 [font](https://www.youtube.com/watch?v=h4Sl21AKiDg)


 New Relic uses a centralize platform collection apps and servers push to. Can create a high load of traffic and actually the monitoring can create a bottleneck if we have many microservices sending information to it. also there is the requirement of installing additional software in each of the microservices to send that data to the centralize collection platform.

 prometheus
 
 prometheus requires only a scraping endpoint, this way metrics can be pulled from several prometheus instances.
 Also pulling its a better way of identifying the health of the service as if the endpoint is not available it's pretty clear the service is not healthy, but if the service doesnt push notifications the reasons might vary and is not as clear its health status. network not working, package got lost etc.

 unable to monitor if the container is short lived with the pull endpoint. For that prometheus uses a push gateway notification 

step learning curve into how to correctly configure prometheus, learning promQL, the query language needed to query database of metrics to end up creating grifana dashboards


pros: reliable
      stand alond and self cotain. it works when part of the infrastructure is down.
      no extensive set up needed
      less complex
      monitor of K8s cluster node resources out of the box
      prometheus components available as docker images
      can be easily deployed in container environment

cons: difficult to scale. Might need several prometheus servers to collect all the metrics if the applications grows. 

In the other hand, this shortage in the numers of metrics collected can be seen as a good point as it forces administrator to think throughfully and narrow down the metrics that are needed for monitoring without just setting metrics that will serve no purpose. 

New relic

[font](https://newrelic.com/platform/kubernetes/monitoring-guide)

pros: Able to see the dashboard (kubernetes cluster explorer) with the kubernetes integration. no need to integrate with other service like kibana or grafana
    automatically deployed agent to pods/nodes???
    access to k8 events
    troubleshoot without the need of switching tools
    integrates with postgres, redis, rabbitMQ, mongoDB

cons: cost $$$$


-----------------------------------------------------------------------

 possible questions to dave

 what are we really trying to achieve with the monitoring? Cluster resource usage, Node availability and health, Application availability and performance?'

 do we use already a tool like grafana o kibana to look at metrics in other services?

 what the average age of feeld containers?

 how many containers are we running in a regular day? is that consider a lot for a prometheus server?

 how many services do we run on average? is there a big change in the number depending on the day of the week?

 do we need to scale up and down those services?