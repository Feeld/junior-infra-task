Prometheus is a free open-source monitoring software that utalises autonomous single server nodes,  trusted by Boxever, Docker, KuberMatic and SoundCloud.

Looks to have exceptional native integration with its Cloud Native Computing Foundation partner Kubernetes as it appears to be the only software actively championed by them.

Prometheus relies on scraping metrics from predefined exposed endpoints that happen via a pull model over HTTP that instruct the server how to scrape it. Although not having. huge native DB, there are third party exporters available for many applications that have an easy way to add web endpoints, such as Kafka and Cassandra.  

Each Prometheus server is standalone, not depending on network storage or other remote services claiming you can rely on it when other parts of the infrastructure are broken, and no extensive setup infrastructure is needed to use it.
