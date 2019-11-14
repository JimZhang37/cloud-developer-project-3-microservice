create:
	eksctl create cluster \
--name prod \
--version 1.14 \
--region us-west-2 \
--nodegroup-name standard-workers \
--node-type t3.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto

run:
	kubectl apply -f env-secret.yaml
	kubectl apply -f aws-secret.yaml
	kubectl apply -f env-configmap.yaml
	kubectl apply -f backend-feed-deployment.yaml
	kubectl apply -f backend-feed-service.yaml
	kubectl apply -f backend-user-deployment.yaml
	kubectl apply -f backend-user-service.yaml
	kubectl apply -f reverseproxy-deployment.yaml
	kubectl apply -f reverseproxy-service.yaml
	kubectl apply -f frontend-deployment.yaml
	kubectl apply -f frontend-service.yaml

runfeed:
	kubectl apply -f env-secret.yaml
	kubectl apply -f aws-secret.yaml
	kubectl apply -f env-configmap.yaml
	kubectl apply -f backend-feed-deployment.yaml
	kubectl apply -f backend-feed-service.yaml

connectfeed:
	kubectl port-forward service/backend-feed 8080:8080

get:
	kubectl get deployment
	kubectl get services
	kubectl get pods

connectback:
	kubectl port-forward service/reverseproxy 8080:8080

connectfront:
	kubectl port-forward service/frontend 8100:8100


delete:
	eksctl delete cluster \
--name prod \
--region us-west-2 \
