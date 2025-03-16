# MongoDB Example Helm Chart

This repository contains a Helm chart for deploying MongoDB. The chart is hosted on GitHub Pages at [mongodb.jotamario.lat](https://mongodb.jotamario.lat).

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
helm repo add quizapp-mongodb https://mongodb.jotamario.lat
helm repo update
helm install my-release quizapp-mongodb/quizapp-mongodb
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the MongoDB chart and their default values.

| Parameter                | Description                           | Default                        |
|--------------------------|---------------------------------------|--------------------------------|
| `replicaCount`           | Number of replicas                    | `1`                            |
| `image.repository`       | MongoDB image repository              | `mongo`                        |
| `image.tag`              | MongoDB image tag                     | `4.4.6`                        |
| `image.pullPolicy`       | Image pull policy                     | `IfNotPresent`                 |
| `service.type`           | Kubernetes service type               | `ClusterIP`                    |
| `service.port`           | MongoDB service port                  | `27017`                        |
| `persistence.enabled`    | Enable persistence using PVC          | `true`                         |
| `persistence.storageClass`| PVC Storage Class for MongoDB volume | `""`                           |
| `persistence.accessMode` | PVC Access Mode for MongoDB volume    | `ReadWriteOnce`                |
| `persistence.size`       | PVC Storage Request for MongoDB volume| `8Gi`                          |
| `mongodbRootPassword`    | MongoDB root password                 | `""`                           |
| `mongodbUsername`        | MongoDB username                      | `""`                           |
| `mongodbPassword`        | MongoDB password                      | `""`                           |
| `mongodbDatabase`        | MongoDB database                      | `""`                           |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example:

```bash
helm install my-release quizapp-mongodb/quizapp-mongodb --set mongodbRootPassword=secretpassword,mongodbUsername=my-user,mongodbPassword=my-password,mongodbDatabase=my-database
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example:

```bash
helm install my-release quizapp-mongodb/quizapp-mongodb -f values.yaml
```

## Accessing MongoDB

Once the chart is deployed, you can access MongoDB using the following command:

```bash
kubectl run --namespace default my-release-mongodb-client --rm --tty -i --restart='Never' --image docker.io/bitnami/mongodb:4.4.6-debian-10-r0 --command -- mongo --host my-release-mongodb
```

## Testing the Deployment

To test the deployment, you can use the following command:

```bash
helm test my-release
```

This will run the test defined in `templates/tests/test-connection.yaml`.

## Cleanup

To delete the deployment, use the following command:

```bash
helm delete my-release
```

This will remove all the Kubernetes components associated with the chart and delete the release.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
