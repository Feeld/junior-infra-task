
## Considerations

### Systems

- Kubernetes
- Containerisation
- GCP
- Postgres
- Redis
- RabbitMQ
- MongoDB

### Self-hosted vs SaaS

- Self-hosting carries a relatively bigger time cost but allows for greater control over the monitoring system
- SaaS carries a higher financial cost but significantly reduces the time required for setup


## Self-hosted

### Icinga

**Pros**

- Fast and flexible general monitoring
- 3rd party plugins for customisation

**Cons**

- There is very little official and recent documentation available on how to integrate Icinga with any of the above considerations
- Its lack of community and popularity in with regards to the stated use cases makes it a less favourable choice

### Zabbix

**Pros**

- Good, customisable data visualisation options
- Clear documentation
- Powerful alerting system
- Good for PostgreSQL and Redis
- Lots of 3rd party solutions

**Cons**

- Similarly to Icinga, there is not a lot of good information on how to use Zabbix with most of the above considerations
- Using Zabbix will likely require another set of monitoring sytems

### Prometheus

**Pros**

- Plenty of information available, good community
- Clear documentation
- Highly performant
- Integrates well with all the listed system requirements
- Has plenty of other integrations which allows for flexibility

**Cons**

- Good data visualisation does not come out of the box - requires Grafana integration
- Uses PromQL, which is another thing to learn
- No support for log management
- Pull system requires secure network configuration 

### Sentry

**Pros**

-

**Cons**

-

### Elastic Cloud on Kubernetes

**Pros**

-

**Cons**

-

## SaaS

### New Relic

**Pros**

-

**Cons**

-

### Google Cloud Stackdriver

**Pros**

-

**Cons**

-

### OpsGenie

**Pros**

-

**Cons**

-

### Datadog

**Pros**

-

**Cons**

-