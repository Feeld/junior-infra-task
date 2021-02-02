
Ensure you're in the prometheus directory, if not ```cd prometheus```.
Run a Kubernetes cluster using minikube then run the following commands to:

To create resources run:
```make create```
To check resources run:
```make get```
Once the rosources are created run:
```make ui```
When the window opens through the browser type and enter {job="prometheus"} to see the metrics
To tidy up, run:
```make delete```