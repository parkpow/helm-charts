# Automatic License Plate Recognition (ALPR, ANPR) on Kubernetes
Get high-accuracy, developer-friendly **automatic license plate recognition** ([ALPR](https://platerecognizer.com/?utm_source=github&amp;utm_medium=website)) or automatic number plate recognition ([ANPR](https://platerecognizer.com/?utm_source=github&amp;utm_medium=website)) on Kubernetes!

Our machine-learning software:

- Works on **dark, low-res, blurry images** and tough angles, all vehicle types, etc.  See our full [ALPR results](https://platerecognizer.com/alpr-results/?utm_source=github&amp;utm_medium=website).
- Works on Video URLs such are RTSP or Video Files
- Decodes **license plate** , vehicle type (e.g. SUV, van, pickup truck), [**vehicle make model**](https://platerecognizer.com/vehicle-make-model-recognition-with-color/?utm_source=github&amp;utm_medium=website) (e.g. Honda Accord), color, and orientation. Ignores bumper stickers, car signs, etc.
- Is optimized for all [50 USA States](https://platerecognizer.com/alpr-for-usa/?utm_source=github&amp;utm_medium=website), [India](https://platerecognizer.com/anpr-for-india?utm_source=github&amp;utm_medium=website), [Brazil](https://platerecognizer.com/anpr-for-brazil/?utm_source=github&amp;utm_medium=website) and [**90+ countries worldwide**](https://platerecognizer.com/countries/?utm_source=github&amp;utm_medium=website).

Get license plate reader deployed on Kubernetes using Helm Charts in under 60 minutes:

- Access a **simple REST API** for easy integration in [8+ programming languages](http://docs.platerecognizer.com/?utm_source=github&amp;utm_medium=website).
- Returns results via **JSON Response** or Webhooks.
- Has [fast inference speed](https://platerecognizer.com/snapshot/#speeds) up to 21 ms.
- Runs on-premise on **Linux,** [**Windows**](https://platerecognizer.com/alpr-on-windows/?utm_source=github&amp;utm_medium=website), Mac, [**Jetson**](https://platerecognizer.com/alpr-on-nvidia-jetson-devices/?utm_source=github&amp;utm_medium=website) **,** [**Kubernetes**](https://platerecognizer.com/anpr-on-kubernetes/?utm_source=github&amp;utm_medium=website), [Raspberry Pi](https://platerecognizer.com/anpr-on-raspberry-pi/?utm_source=github&amp;utm_medium=website), [Zynq](https://platerecognizer.com/alpr-for-xilinx-zynq/?utm_source=github&amp;utm_medium=website), [96Boards](https://platerecognizer.com/alpr-for-96boards/?utm_source=github&amp;utm_medium=website), [LattePanda](https://platerecognizer.com/anpr-on-lattepanda/?utm_source=github&amp;utm_medium=website) and more.

ALPR, ANPR software on Kubernetes is ideal for parking, toll, police surveillance, community security, and other use cases.

Our license plate recognition (LPR) software can also forward results to our full **ALPR Dashboard** and [**Parking Management software**](https://parkpow.com/?utm_source=github&amp;utm_medium=website) solution, ParkPow.

Sign up for a [**Free Trial**](https://app.platerecognizer.com/accounts/signup/?utm_source=github&amp;utm_medium=website) now (no credit card required) or **learn more** at [https://platerecognizer.com](https://platerecognizer.com/).

![Plate-Recognizer-ALPR-ANPR-Github-Kubernetes](https://user-images.githubusercontent.com/61606720/103374983-c0c65680-4a8d-11eb-99ac-8e0867d3b77f.jpg)

## Installation
Instructions to install Plate Recognizer [Snapshot](https://platerecognizer.com/snapshot/?utm_source=github&amp;utm_medium=website) or [Stream](https://platerecognizer.com/STREAM/?utm_source=github&amp;utm_medium=website) SDK on Kubernetes cluster. Requirements:
1. Setup your Kubernetes cluster. For example, https://kubernetes.io/docs/tasks/tools/install-minikube/
	- If using Minikube, make sure to enable the following addons `dashboard ingress helm-tiller`
1. Get helm from https://github.com/helm/helm/releases
1. Clone this repository `git clone https://github.com/parkpow/helm-charts.git` and `cd helm-charts`

### Snapshot SDK
1. [Contact support](https://platerecognizer.com/contact/) to **enable Kubernetes** for your account. License without Kubernetes enabled requires a persistent volume: `persistence.enabled=true`
1. Install chart `helm install platerec-snapshot snapshot/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`


#### Configuration

- To **upgrade** the chart, do `helm upgrade platerec-snapshot snapshot/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`
- To **delete** the deployment, do `helm delete platerec-snapshot`
- To use the **gpu version** instead of the cpu version, do `helm install platerec-snapshot snapshot/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY> --set image.repository=platerecognizer/alpr-gpu` 
- To **deploy** to a different namespace other than `default`, include `--namespace <namespace-name>` to the install/upgrade command as so  `helm install platerec-snapshot snapshot/ --namespace <namespace-name> --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`

---

**Configurations variables** that can be changed (by adding them to the install command using `--set` parameter)

| Parameter | Description | Default  | Options |
|-----------|-------------|----------|---------|
| `TOKEN`   |  PlateRecognizer Token (**required**)            | `nil`          |    |
| `LICENSE_KEY`   |  PlateRecognizer Snapshot License (**required**)            | `nil`          |    |
| `replicaCount`   |  Number of Pods to run            | `1`          |   |
| `image.repository`   | Plate Recognizer sdk             | `platerecognizer/alpr`          | Any from [Command Selector](https://guides.platerecognizer.com/docs/snapshot/manual-install) |
| `image.pullPolicy`   |   Image pull policy   | `Always`          | [`Always`, `IfNotPresent`] |
| `image.pullSecrets`   |  	Specify docker-registry secret names as an array            | `[]`          | `True` |
| `service.annotations`                     | Service annotations                                                                                    | `{}`                                                         |
| `service.type`                            | Kubernetes Service type                                                                                | `ClusterIP`                                               | [`LoadBalancer`, `ClusterIP`]
| `service.port`                            | Service HTTP port                                                                                      | `8080`                                                         |
| `persistence.enabled`                     | Enable persistence using PVC                                                                           | `false`                                                       |
| `persistence.existingClaim`               | Enable persistence using an existing PVC                                                               | `nil`                                                        |
| `persistence.storageClass`                | PVC Storage Class                                                                                      | `nil` (uses alpha storage class annotation)                  |
| `persistence.accessMode`                  | PVC Access Mode                                                                                        | `ReadWriteOnce`                                              | [`ReadWriteMany`, `ReadWriteOnce` ]
| `persistence.size`                        | PVC Storage Request                                                                                    | `1Gi`                                                       |


### Stream SDK
Install chart `helm install platerec-stream stream/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`

#### Configuration
- Update Stream config by editing `configmap.yaml` then restart services for changes to take effect by upgrading the chart. 
	> To use Stream configuration through Cloud, disable the configmap volume mount so configs get loaded from Cloud on container start.
- To **upgrade** the chart, do `helm upgrade platerec-stream stream/ --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`
- To **delete** the deployment, do `helm delete platerec-stream`
- To **deploy** to a different namespace other than `default`, include `--namespace <namespace-name>` to the install/upgrade command as so  `helm install platerec-stream stream/ --namespace <namespace-name> --set TOKEN=<MY_TOKEN> --set LICENSE_KEY=<LICENSE_KEY>`

---

**Configurations variables** that can be changed (by adding them to the install command using `--set` parameter)

| Parameter | Description | Default  | Options |
|-----------|-------------|----------|---------|
| `TOKEN`   |  PlateRecognizer Token (**required**)            | `nil`          |    |
| `LICENSE_KEY`   |  PlateRecognizer Stream License (**required**)            | `nil`          |    |
| `fileUpload`   |  Enable service for File Upload            | `false`          | [`true`, `false`]  |
| `image.repository`   | Plate Recognizer sdk             | `platerecognizer/alpr-stream`          | Any from [Command Selector](https://guides.platerecognizer.com/docs/stream/manual-install#docker-command-selector) |
| `image.pullPolicy`   |   Image pull policy   | `Always`          | [`Always`, `IfNotPresent`] |
| `image.pullSecrets`   |  	Specify docker-registry secret names as an array            | `[]`          | `True` |
| `service.annotations`                     | Service annotations                                                                                    | `{}`                                                         |
| `service.type`                            | Kubernetes Service type                                                                                | `ClusterIP`                                               | [`LoadBalancer`, `ClusterIP`]
| `service.port`                            | Service HTTP port                                                                                      | `8080`                                                         |
| `persistence.existingClaim`               | Enable persistence using an existing PVC                                                               | `nil`                                                        |
| `persistence.storageClass`                | PVC Storage Class                                                                                      | `nil` (uses alpha storage class annotation)                  |
| `persistence.accessMode`                  | PVC Access Mode                                                                                        | `ReadWriteOnce`                                              | [`ReadWriteMany`, `ReadWriteOnce` ]
| `persistence.size`                        | PVC Storage Request                                                                                    | `10Gi`                                                       |

> The service options only apply when `fileUpload=true`

## Minikube Notes
To access the instance when using a custom cluster in Minikube, run the following command:

- Simulate a load balancer `minikube tunnel`
- Then run the commands shown after the `helm install` command.
- You can also use this command to get the extenal_id `kubectl get --namespace default svc -w platerec-sdk-test-platerec-helm`
- Finally call the SDK endpoint with `curl -F 'upload=@/path/to/car.jpg' http://<external_ip>:8080/alpr`
- Another option of accessing minikube services `minikube service platerec-stream`
