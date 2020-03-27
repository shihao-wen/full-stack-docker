# Full-Stack-MicroServices
Docker + Kubernetes + CI/CD

## Docker
```bash
docker run --rm --publish 8080:8080 -v $HOME/.aws:/root/.aws --env POSTGRESS_HOST=$POSTGRESS_HOST --env POSTGRESS_USERNAME=$POSTGRESS_USERNAME --env POSTGRESS_PASSWORD=$POSTGRESS_PASSWORD --env POSTGRESS_DB=$POSTGRESS_DB --env AWS_REGION=$AWS_REGION --env AWS_PROFILE=$AWS_PROFILE --env AWS_BUCKET=$AWS_BUCKET --env JWT_SECRET=$JWT_SECRET --name feed <your_dockerhub_username_lowercase>/udacity-restapi-feed
```
Publish to Dockerhub:
```bash
docker push yourdockerhubname/udacity-restapi-feed
docker push wenshihao1993/udacity-restapi-feed
```
Docker-compose:
```bash
docker-compose -f docker-compose-build.yaml build --parallel
docker-compose up
docker-compose up -d 
```
![DockerHub](/images/DockerHub.png)
After Verification: http://localhost:8100
```bash
docker-compose stop
docker-compose down
```

## Secret and Credentials
Converting each String manually, put into yaml file and create the secret.
```bash
echo -n <String to convert> | base64
kubectl apply -f ./env-configmap.yaml
kubectl apply -f ./env-secret.yaml
kubectl apply -f ./aws-secret.yaml
```
Check the list of Secrets using 
```bash 
kubectl get secrets
```

## Kubernetes
```bash
kubectl apply -f reverseproxy-deployment.yaml
kubectl get deployment
kubectl get rs
kubectl get pod
```
Deploy the Pods and ReplicaSets:
```bash
kubectl apply -f aws-secret.yaml
kubectl apply -f env-configmap.yaml
kubectl apply -f env-secret.yaml
kubectl apply -f reverseproxy-service.yaml
kubectl apply -f frontend-service.yaml
kubectl apply -f backend-feed-service.yaml
kubectl apply -f backend-user-service.yaml
kubectl apply -f backend-feed-deployment.yaml 
kubectl apply -f backend-user-deployment.yaml 
kubectl apply -f frontend-deployment.yaml 
kubectl apply -f reverseproxy-deployment.yaml
kubectl apply -f pod-example/pod.yaml
```
Check the Status of Pods:
```bash
kubectl get pod -o wide
# or
kubectl describe pods <pod name>
```
![pods](/images/Kubernetes_pod.png)
```bash
port-forward pod/<pod name> 8100:8100
```