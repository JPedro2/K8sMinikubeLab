# Install minikube on MacOs
* Reference linkhttps://github.com/kubernetes/minikube/blob/v0.15.0/README.md* Requirements	* homebrew (updated)	* virtual box### System Prep MAC
Download and install Minikube from the latest release

https://github.com/kubernetes/minikube/releases

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.17.1/minikube-darwin-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
Install Kubectl from googleReference:  https://kubernetes.io/docs/tasks/kubectl/install/

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl```Make it executable and move to your path (e.g. /usr/local/bin) ```
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl ```### System Prep for Windows Versions before 10
Upgrade Windows. Seriously. Upgrade it. Or better yet buy a Mac!

The best way to get this part lab working is to download Ubuntu Desktop and load int in a virtualbox (or VMWare) virtual machine. Trying to get all of the components working together natively is not easy and will not be supported in the lab. It does work in a VM. 

* Load Virtual Box https://www.virtualbox.org/wiki/Downloads
* download ISO image for Ubuntu 16.10 Desktop https://www.ubuntu.com/download/desktop
* Install Docker for ubuntu following these instructions https://store.docker.com/editions/community/docker-ce-server-ubuntu?tab=description
* Install Virtualbox https://tecadmin.net/install-oracle-virtualbox-on-ubuntu/#

Install Kubectl from googleReference:  https://kubernetes.io/docs/tasks/kubectl/install/

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl```Make it executable and move it to PATH

```
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```Install Minikube```curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.17.1/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

 ### System Prep Windows 10* Make sure hyper-v is enabled
* Docker windows is installedInstall Kubectl from googleReference:  https://kubernetes.io/docs/tasks/kubectl/install/

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/windows/amd64/kubectl.exe``````https://storage.googleapis.com/kubernetes-release/release/${K8S_VERSION}/bin/${GOOS%7D/$%7BGOARCH%7D/$%7BK8S_BINARY%7D
```
## Start Minikubee.	$minikube start --vm-driver virtualboxi.	This will download minikube ISO an create a VM under vbox```eval $(minikube docker-env)
```

Setup Kubectl to access Cluster

Download kubectl client from here: https://github.com/eirslett/kubectl-windows/releases
Put it in a place that you want to add to your path and add that place to your path
Proceed with installing your local Kubernetes cluster in the next step. It will setup the kube-config so that you may use kubectl like normal from CMD
Setup Kubernetes Cluster

Install Minikube by downloading the minikube-installer.exe from here: https://github.com/kubernetes/minikube/releases
Execute the installer
Execute the update_path.bat in the installation folder under C:\Program Files x86\Kubernetes\Minikube
Create a HyperV Virtual Switch by openning up the HyperV Manager from the Start menu and right-clicking on your computers node in the left pane. Then select „Manage virtual switches“ and create a new virtual switch that goes by the name „minikube“ and is set to „internal only“. The result should look like so:

Start Minikube by pointing it towards hyperv and the newly created hyperV switch: minikube start --vm-driver=hyperv --hyperv-virtual-switch=minikube
Optionally: Provide the amount of CPUs and Memory you would like to give to the minikube VM with the –cpus and –memory flags. I.e.: minikube start --vm-driver=hyperv --hyperv-virtual-switch=minikube --cpus=4 --memory=4096