## MINIKUBE

## Learn
from https://www.youtube.com/watch?v=kWMBSySuLhU  

## check virtualization is supported on mac os
sysctl -a | grep -E --color 'machdpe.cpu.features|VMX'  

## install kubectl  
brew install kubectl  

## install hypervisor  
brew install hyperkit  

## install minikube  
brew install minikube  

## start minikube  
minikube start --driver=<driver_name> (for example hyperkit)  

## check status minikube  
minikube status  

## check cluster info  
kubectl cluster-info  

## check nodes  
kubectl get nodes  

## stop minikube  
minikube stop  

## use local docker  
eval $(minikube docker-env)  

## go to pod  
kubectl exec -it project-mysql-fcdd7cd78-n964k /bin/sh  
kubectl exec -it project-mysql-fcdd7cd78-n964k bash  

## mysql  
https://medium.com/@midejoseph24/deploying-mysql-on-kubernetes-16758a42a746  

## redis  
https://medium.com/@ilyash/how-to-deploy-php-redis-application-to-kubernetes-using-minikube-1c7129245a5d  

## monitoring  
kubectl get nodes  
kubectl -n develop get pods  
kubectl top node minikube  
kubectl top pod project-backend-user-golang-596bbb47ff-5wgfm  
minikube addons enable metrics-server  
install metric server kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml  
kubectl get ns  
kubectl -n kube-system get pods  
kubectl top node minikube  
kubectl describe node minikube  
kubectl get pods  
kubectl get pods -o wide  
kubectl top pod project-backend-user-golang-596bbb47ff-5wgfm  
kubectl describe project-backend-user-golang-596bbb47ff-5wgfm  