# Tag docker image 

create:

	kubectl apply -f namespace.yml
	kubectl apply -f config-map.yml
	kubectl apply -f rbac.yml
	kubectl apply -f deployment.yml
	kubectl apply -f node-service.yml
	kubectl apply -f node-exporter-daemonset.yml
	# To access metrics from promenteus and node-exporter we replace the config.
	kubectl replace -f config-map-2.yml

ui:

	minikube service --namespace=monitoring prometheus

get:

	minikube service list

delete:

	kubectl delete namespace monitoring
