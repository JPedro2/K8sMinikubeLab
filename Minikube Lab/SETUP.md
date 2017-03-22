# Install minikube on MacOs
* Reference linkhttps://github.com/kubernetes/minikube/blob/v0.15.0/README.md* Requirements	* homebrew (updated)	* virtual box## System Prep MAC
Download and install Minikube from the latest release

https://github.com/kubernetes/minikube/releases

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.17.1/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
Install Kubectl from googleReference:  https://kubernetes.io/docs/tasks/kubectl/install/

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl```Make it executable and move to your path (e.g. /usr/local/bin) ```
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl ```### System Prep Windows 10Install Kubectl from googleReference:  https://kubernetes.io/docs/tasks/kubectl/install/

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/windows/amd64/kubectl.exe```## Start Minikubee.	$minikube start --vm-driver virtualboxi.	This will download minikube ISO an create a VM under vbox