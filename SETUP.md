# Install minikube on MacOs
* Reference link
Download and install Minikube from the latest release

https://github.com/kubernetes/minikube/releases

``
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.17.1/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
Install Kubectl from google

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl 

* Load Virtual Box https://www.virtualbox.org/wiki/Downloads
Install Docker toolbox
Install Kubectl from google
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/windows/amd64/kubectl.exe
download executable file and installer
```

 
* Load Virutalbox
* Docker windows is installed

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/windows/amd64/kubectl.exe
download executable file and installer
```

``` 
$minikube start --vm-driver=virtualbox --cpus=4 --memory=4096
This will download minikube ISO an create a VM under vbox
```
This command will point your local docker cli command to docker running on the kubernetes cluster

Minikube status

Minikube ip

Minikube dashboard

Kuberctl version