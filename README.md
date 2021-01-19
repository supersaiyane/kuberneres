# kuberneres
My kubernetes Learning

Launch A Single Node Cluster

step 1 - start minikube
```
minikube version
minikube start --wait=false
```
Step 2 - Cluster Info
```
kubectl cluster-info
```
To view the nodes in the cluster using, If the node is marked as NotReady then it is still starting the components.
```
kubectl get nodes
```
Step 3 - Deploy Containers

Using kubectl run, it allows containers to be deployed onto the cluster - 
```
kubectl create deployment first-deployment --image=katacoda/docker-http-server
```
The status of the deployment can be discovered via the running Pods - 
```
kubectl get pods
```

Once the container is running it can be exposed via different networking options, depending on requirements. One possible solution is NodePort, that provides a dynamic port to a container.
```
kubectl expose deployment first-deployment --port=80 --type=NodePort
```
The command below finds the allocated port and executes a HTTP request.
```
export PORT=$(kubectl get svc first-deployment -o go-template='{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}')
echo "Accessing host01:$PORT"
curl host01:$PORT
```

Step 4 - Dashboard

Enable the dashboard using Minikube with the command 
```
minikube addons enable dashboard
```
Make the Kubernetes Dashboard available by deploying the following YAML definition. This should only be used on Katacoda.
```
kubectl apply -f /opt/kubernetes-dashboard.yaml
```
The Kubernetes dashboard allows you to view your applications in a UI. In this deployment, the dashboard has been made available on port 30000 but may take a while to start.
To see the progress of the Dashboard starting, watch the Pods within the kube-system namespace using 
```
kubectl get pods -n kubernetes-dashboard -w
```
Once running, the URL to the dashboard is https://2886795288-30000-ollie07.environments.katacoda.com/

Launch a multi-node cluster using Kubeadm

