# pre-requisite 

open docker desktop,
make sure engine is running

# run  : 
winget install Kubernetes.minikube 

winget install kubernetes.kubectl

# create file names nginx-pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80



# open terminal and run
minikube start --driver=docker 
minikube status 
kubectl get nodes 
kubectl apply -f nginx-pod.yaml 
kubectl get pods 
kubectl describe pod nginx-pod 
kubectl port-forward pod/nginx-pod 8085:80 
# Open http://localhost:8085 in a browser. 
# Keep port-forward running while testing.

# open another teminal and run

kubectl delete pod nginx-pod 

kubectl create deployment my-nginx --image=nginx 
kubectl get deployments 
kubectl get pods


kubectl scale deployment my-nginx --replicas=3 
kubectl get pods 

kubectl set image deployment/my-nginx nginx=nginx:1.25 
kubectl rollout status deployment/my-nginx 
kubectl rollout undo deployment/my-nginx

# extra 
kubectl expose deployment my-nginx --type=NodePort --port=80
kubectl get svc
minikube service my-nginx --url

