## Installation

Instructions to install the Plate Recognizer SDK on your Kubernetes cluster.

1. Get helm from https://github.com/helm/helm/releases
1. Setup your Kubernetes cluster. For example, https://kubernetes.io/docs/tasks/tools/install-minikube/
	- If using Minikube, make sure to enable the following addons `dashboard ingress helm-tiler`
1. Clone this repository `git clone https://github.com/parkpow/helm-charts.git` and `cd helm-charts`
1. Install the chart `helm install platerec-sdk platerec-helm/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`

### Configuration

- To **upgrade** the chart, do `helm upgrade platerec-sdk platerec-helm/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`
- To **delete** the deployment, do `helm delete platerec-sdk`
- To use the **gpu version** instead of the cpu version, do `helm install platerec-sdk platerec-helm/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY> --set image.repository=platerecognizer/alpr-gpu` 
- To **deploy** to a different namespace other than `default`, include `--namespace <namespace-name>` to the install/upgrade command as so  `helm install platerec-sdk platerec-helm/ --namespace <namespace-name> --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`

here are a few configurations variables that can be changed (by adding them to the install command using `--set` parameter)
| Parameter | Description | Default  | Options |
|-----------|-------------|----------|---------|
| `TOKEN`   |  PlateRecognizer Token (required)            | `nil`          |    |
| `LICENSE_KEY`   |  PlateRecognizer SDK License (required)            | `nil`          |    |
| `replicaCount`   |  Number of Pods to run            | `1`          |   |
| `image.repository`   | Plate Recognizer sdk             | `platerecognizer/alpr`          | [`platerecognizer/alpr`, `platerecognizer/alpr-gpu`]  |
| `image.pullPolicy`   |   Image pull policy   | `Always`          | [`Always`, `IfNotPresent`] |
| `image.pullSecrets`   |  	Specify docker-registry secret names as an array            | `[]`          | `True` |
| `service.annotations`                     | Service annotations                                                                                    | `{}`                                                         |
| `service.type`                            | Kubernetes Service type                                                                                | `ClusterIP`                                               | [`LoadBalancer`, `ClusterIP`]
| `service.port`                            | Service HTTP port                                                                                      | `8080`                                                         |
| `persistence.enabled`                     | Enable persistence using PVC                                                                           | `true`                                                       |
| `persistence.existingClaim`               | Enable persistence using an existing PVC                                                               | `nil`                                                        |
| `persistence.storageClass`                | PVC Storage Class                                                                                      | `nil` (uses alpha storage class annotation)                  |
| `persistence.accessMode`                  | PVC Access Mode                                                                                        | `ReadWriteOnce`                                              | [`ReadWriteMany`, `ReadWriteOnce` ]
| `persistence.size`                        | PVC Storage Request                                                                                    | `10Gi`                                                       |






### Minikube Notes

To access the instance when using a custom cluster in Minikube, run the following command:

- Simulate a load balancer `minikube tunnel`
- Then run the commands shown after the `helm install` command.
- You can also use this command to get the extenal_id `kubectl get --namespace default svc -w platerec-sdk-test-platerec-helm`
- Finally call the SDK endpoint with `curl -F 'upload=@/path/to/car.jpg' http://<external_ip>:8080/alpr`


