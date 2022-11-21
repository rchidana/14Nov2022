# Minikube & kubectl set-up on Ubuntu 20.04

### Steps to Install Minukube to run Kubernetes Version 1.25.3 on Ubuntu 20.04

Install latest stable Kubectl

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
```

List all available versions of kubectl so that you can choose the version that you need
```
sudo apt list kubectl* -a

```

Let us install latest kubectl version for our Lab exercises

```
sudo apt-get install kubectl
```

For specific versions of kubectl, specify the version as below

sudo apt-get install kubectl=1.17.0-00

Check kubectl version
```
kubectl version --client -o json
kubectl version --client -o yaml
```

Minikube Documentation : https://minikube.sigs.k8s.io/docs/start/

Install Minikube latest version 

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
sudo install minikube /usr/local/bin

```

Start Minikube single node cluster by specifying docker Driver and with Kubernetes version v1.25.3
```
minikube start --vm-driver=docker --kubernetes-version=v1.25.3
```


Get cluster info using kubectl
```
kubectl get nodes
kubectl get po --all-namespaces
```

Let us run a sample deployment & check our set up
```
kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080
kubectl expose pod hello-minikube  --type=NodePort

kubectl get pod
minikube service hello-minikube 
```

This will open up a web browser and hit the service URL
If everything is OK, let us delete our pod & service
```
kubectl delete po hello-minikube
kubectl delete svc hello-minikube
```

## Congratulations, your minikube set-up is Successfull!!!
