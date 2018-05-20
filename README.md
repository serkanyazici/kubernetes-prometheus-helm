# KUBERNETES PROMETHEUS-OPERATOR HELM

This repository aims to deploy an application by Helm using Google Container Engine and collect the application metrics by Prometheus. HAProxy (1.8) is used as application with a little hack. You can check application configuration within docker folder.

See also: https://hub.docker.com/r/waidmannsheil/haproxy/

### REQUIREMENTS

- Kubernetes Cluster (GKE 1.8 or higher)
- Helm installed
- Executing user must have 'cluster-admin' role

### INSTALLATION

Apply the following steps in order:

`helm install --name nginx-ingress stable/nginx-ingress --set rbac.create=true`

`helm install helm-zoover/`

`kubectl apply -f prometheus-operator/bundle.yaml`

`kubectl create -f prometheus-operator/exporter-service.yaml -f prometheus-operator/servicemonitor.yaml -f prometheus-operator/prometheus-rbac.yaml -f prometheus.yaml -f prometheus-frontend.yaml`

### USAGE

First step of the installation will create a LoadBalancer for your cluster, you can see your LoadBalancer's External-IP address such:

`kubectl get service nginx-ingress-controller`

Access the application:

`http://<External-IP>/example-proxy`

`http://<External-IP>/metrics` [zoover:devops]

(https requests might throw an error due to certificate reasons however you can still proceed or provide your own)

Access the Prometheus UI:

`http://<NodeIP>:30900`

You can also get a list of External-IPs of your nodes by typing the command below, just use one from the output for Prometheus UI.

`kubectl get nodes --selector=kubernetes.io/role!=master -o jsonpath={.items[*].status.addresses[?\(@.type==\"ExternalIP\"\)].address}`

Happy Helming!
