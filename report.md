# Report

## Considerations

- Kubernetes
- Containerisation
- GCP
- Postgres
- Redis
- RabbitMQ
- MongoDB


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

- Plenty of clear documentation available, good community
- Highly performant
- Integrates well with all the listed system requirements
- Has plenty of other integrations which allows for flexibility

**Cons**

- Good data visualisation does not come out of the box - requires Grafana integration
- Uses PromQL, which is another thing to learn
- No support for log management
- Pull system requires secure network configuration 

### Nagios

**Pros**

- Offers PostgreSQL support natively but not much else, in terms of the requirements above
- Flexibile
- Log managemnent
- Lots of community plugins

**Cons**

- Steep learning curve
- Does not offer many out of the box integrations for the requirements above


## SaaS

### New Relic

**Pros**

- Native support for all system requirements
- As with Prometheus, there are lots of other native integrations
- Granular metrics
- Good data visualisation options

**Cons**

- Lots of options can be overwhelming
- Can get expensive with limited free options

### Google Cloud Stackdriver (now Google Cloud Operations Suite)

**Pros**

- Native support for GCP, GKE, Redis
- Real-time log analysis
- Scalable and fully managed
- Hybrid and multi-cloud support

**Cons**

- Requires Blue Medora integration for PostgreSQL, MongoDB and RabbitMQ support
- Search can be slow, particularly old logs
- Unless configured differently, logs are unavailable after 30 days by default
- Pricing can be hard to estimate

### OpsGenie

**Pros**

- Handles alert managaement well
- Offers on-call scheduling
- Provides performance analytics

**Cons**

- Does not seem well suited to our use case – it is an escalation management and notification system

### Datadog

**Pros**

- Integrates with all the system requirements
- Great flexibility and extensibility
- Active community support
- Fast and powerful 
- Log management
- Good data visualisation

**Cons**

- Heavy customisation may be overwhelming
- Steep learning curve
- Documentation isn't always great


## Conclusion

From each category, I would recommend Prometheus and Datadog for their flexibility, community support and excellent choice of integrations. Both options fully satisfy the system requirements. For the purposes of picking one option, my reasoning would depend on many other things such as team size, budget, business need and so on.

Using Feeld as an example, I would pick Datadog as the configuration and maintenance of a self-hosted option could be cumbersome for a small and busy platforming team. Datadog would be responsible for patching and upgrading their services, something which may incur both time and financial costs if a self-hosted tool is used. The myriad of integration options helps avoid vendor lock-in and allows for customisation, which is good for a growing business that may require a change in technology.

As Feeld is fully remote, being able to access Datadog on any device could be a good feature to have, as of course, infrastructure management sometimes presents problems out of regular working hours.

One notable downside with using a SaaS option is that given the sensitive data that Feeld manages, lack of control over security measures may present issues. I also acknowledge that SaaS tools come with a financial cost, as opposed to the free/open-source nature of self-hosted options, but I believe the pros outweigh the cons.

