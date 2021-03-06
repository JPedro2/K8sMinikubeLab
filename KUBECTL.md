# A gentle tour of ```KUBECTL```


## 0. Goals
The goals of this lab are for you to use ```kubectl``` to communicate with your local instance of kubernetes as if it was a big kubernetes cluster. You will run a few basic kubectl commands to show key concepts. This lab seeks to be a gentle introduction to kubernetes.  

## 1. working with ```Kubectl```

You are now ready to interact with your cluster.  Try a few commands.

### 1.1. Get nodes in the cluster:

We can see how many nodes are defined in our cluster.

```
kubectl get nodes
```

### 1.2.  Get general cluster information

Get the cluster info:

```
kubectl cluster-info
```
Get the component status:

```
kubectl get componentstatuses
```

### 1.3.  Get help from kubernetes!
Have a question about what one of the resources does?  You can have kubectl explain it to you:

```
kubectl explain pods
```
As usual you can also run the -h flag after any sub command to find more about the topic.

```
kubectl rolling-update -h
```

### 1.4.  See what containers/pods are running

Now let's see what's running in the cluster:

```
kubectl get pods
```

Here you may not see anything running because by default you're only looking at pods in your own namespace.  

Let's see what's running outside your namespace:

```
kubectl get pods --all-namespaces
```

You can also see where the pods are running.  This helps with troubleshooting.  

```
kubectl get pods -o wide --all-namespaces
```

### 1.5. follow the changes

If you are familiar with the linux ```tail -f``` command or ```watch``` command, kubernetes has a great way of monitoring changes by using a ```-w``` option at the end of the ```get pods``` command.  This is done by running the command:

```
kubectl get pods -o wide --all-namespaces -w
```
You can watch for any changes as other lab participants create pods.  To exit this command type ```control+c``` or while holding down the control key on your computer tap the 'c' key.

## 2. Run containers with ```kubectl```

In this section we'll run a few commands to manipulate pods and containers.

### 2.1.  Start up busybox

Start up a simple [busybox](https://busybox.net/about.html) deployment by running:

```
kubectl run bb --image=busybox --command -- sleep 3600
```

This command creates

* A deployment named ```bb```
* A pod that runs with the deployment.

### 2.2. Verify busybox

Check for your self that these are running:

```
kubectl get deployments
kubectl get pods
```
You'll see there is a deployment named ```bb``` and a pod running called ```bb-<some-random-stuff>```.  

The deployment states the intent of the pods.  By default we only ran one instance of the busybox container.  

### 2.3. Try to kill a pod

Let's see what happens when we try to kill the busybox pod:

```
kubectl get pods
```
Make note of your busybox pod.  (It will be something like ```bb-209343k43-core79```.)

Kill the running pod:

```
kubectl delete pod <name of your pod>
```
e.g: ```kubectl delete pod bb-209343k43-core79```.

Now look at the pods again:

```
kubectl get pods
```

Did the pod go away?  What happened?  Why?  

### 2.4. Examine busybox deployment

Everytime you killed a pod in the previous step Kubernetes brought up a new one in its place.  This is because the ``kubectl run`` command you ran above created a [deployment](http://kubernetes.io/docs/user-guide/deployments/).

Take a look at the deployment you created:

```
kubectl describe deployment bb
```

This makes sure that there is always at one busybox pod running. Deployments used to be called replication controllers.  They control how the pods run.  

## 3. Further Pod Exploration

These commands are used during debuggging and are pretty handy for figuring out what is going on with applications in your system.

### 3.1. Show logs

We can show the logs of a container.  Run the command:

```
kubectl logs <pod name>
```
where ```<pod name>``` is the name of the running busybox container.

Now since busybox doesn't have any logs, you won't see anything in the output, but if you were running something like nginx or another service you would see all the great logs from this.

### 3.2. Exploring a running container

We can also attach to a running pod and see what's happening inside of it.  Attach to your busy box container by running:

```
kubectl exec -it bb-2097322085-mv9ab -- /bin/sh
```
This will drop you into the busybox shell on the container.  Here we can run commands to explore how the container was set up:

```
cat /etc/resolv.conf
```
You'll see that there is ```cluster.local``` and several other kubernetes DNS settings in there, including your namespace.  You'll also notice that the nameserver is set to ```10.32.0.10```.  This is the service that was set up prior and is running in a container.  

To show that DNS is functioning, try resolving the name of the dashboard:

```
nslookup kubernetes-dashboard.kube-system.svc.cluster.local
```
Here you can see that DNS tells us the cluster IP of the server.  We can also do a ```wget``` to grab the dashboard web page:

```
wget kubernetes-dashboard.kube-system.svc.cluster.local:9999
```
We use port 9999 because that was what we specified in the kubernetes-dashboard deployment that was run earlier.

You won't be able to ping this service because the kube-proxy service that runs on each host only forwards the specified port with tcp.  ICMP queries don't go through.  

Exit out of the busybox container

```
exit
```
### 3.3.  Delete the busybox Deployment

You should now be back on your workstation.

Delete the busybox deployment.  This will also delete the pods.

```
kubectl delete deployment bb
```
Make sure there are no pods left by running:

```
kubectl get pods
```
The output should be empty.  Good job!


You are done!  Go back to the [Main Page](README.md)
