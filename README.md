## Installation

1. Get helm from https://github.com/helm/helm/releases
1. Setup your Kubernetes cluster. For example, https://kubernetes.io/docs/tasks/tools/install-minikube/
	- If using Minikube, make sure to enable the following addons `dashboard ingress helm-tiler`
1. Install the chart`helm install platerec-sdk platerec-helm/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`

### Configuration

- To **upgrade** the chart, do `helm upgrade platerec-sdk platerec-helm/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`
- To **delete** the deployment, do `helm delete platerec-sdk`
- To use the **gpu version** instead of the cpu version, do `helm install platerec-sdk platerec-helm/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY> --set image.repository=platerecognizer/alpr-gpu` 

### Minikube Notes

To access the instance when using a custom cluster in Minikube, run the following command:

- Simulate a load balancer `minikube tunnel`
- Then run the commands shown after the `helm install` command.
- You can also use this command to get the extenal_id `kubectl get --namespace default svc -w platerec-sdk-test-platerec-helm`
- Finally call the SDK endpoint with `curl -F 'upload=@/path/to/car.jpg' http://<external_ip>:8080/alpr`


