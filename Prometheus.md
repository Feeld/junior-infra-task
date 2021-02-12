Prometheus is a free open-source monitoring software that utilises autonomous single server nodes, trusted by Boxever, Docker, KuberMatic and SoundCloud.

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
