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

## install grafana prometheus kube-state-metrics node-exporter
brew install helm
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts  
helm repo update  
helm install prometheus prometheus-community/kube-prometheus-stack  

## create prometheus-configmap.yaml
kubectl apply -f prometheus-configmap.yaml

## install kube-state-metrics node-exporter  
helm install kube-state-metrics prometheus-community/kube-state-metrics  
NAME: kube-state-metrics  
LAST DEPLOYED: Wed May 22 20:58:37 2024  
NAMESPACE: default  
STATUS: deployed  
REVISION: 1  
TEST SUITE: None  
NOTES: 
kube-state-metrics is a simple service that listens to the Kubernetes API server and generates metrics about the state of the objects.  
The exposed metrics can be found here:  
https://github.com/kubernetes/kube-state-metrics/blob/master/docs/README.md#exposed-metrics  

The metrics are exported on the HTTP endpoint /metrics on the listening port.  
In your case, kube-state-metrics.default.svc.cluster.local:8080/metrics  

They are served either as plaintext or protobuf depending on the Accept header.  
They are designed to be consumed either by Prometheus itself or by a scraper that is compatible with scraping a Prometheus client endpoint.  

helm install node-exporter prometheus-community/prometheus-node-exporter  
NAME: node-exporter  
LAST DEPLOYED: Wed May 22 20:59:10 2024  
NAMESPACE: default  
STATUS: deployed  
REVISION: 1  
TEST SUITE: None  
NOTES:  
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=prometheus-node-exporter,app.kubernetes.io/instance=node-exporter" -o jsonpath="{.items[0].metadata.name}")  
  echo "Visit http://127.0.0.1:9100 to use your application"  
  kubectl port-forward --namespace default $POD_NAME 9100  

## access prometheus  
kubectl port-forward svc/prometheus-kube-prometheus-prometheus 9090:9090  
Status > Targets  

## install grafana  
helm repo add grafana https://grafana.github.io/helm-charts  
helm repo update  
helm search repo grafana  
helm install grafana grafana/grafana  
helm list  
kubectl port-forward svc/grafana 3000:80
grafana user: admin, password: kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo  zSORYZzFSGqtTRL3tygwckBNtjCqV2vndXgKsnmT  

## remove instalation
helm list  
helm uninstall grafana  
helm uninstall kube-state-metrics  
helm uninstall node-exporter  
helm uninstall prometheus  

kubectl get all -l release=grafana  
kubectl delete deployment -l release=grafana  
kubectl delete service -l release=grafana  
kubectl delete configmap -l release=grafana  
kubectl delete secret -l release=grafana  
kubectl delete pvc -l release=grafana

kubectl get all -l release=prometheus  
kubectl delete deployment -l release=prometheus  
kubectl delete service -l release=prometheus  
kubectl delete configmap -l release=prometheus  
kubectl delete secret -l release=prometheus  
kubectl delete pvc -l release=prometheus  
  
helm repo list  
helm repo remove prometheus-community  
kubectl get all  