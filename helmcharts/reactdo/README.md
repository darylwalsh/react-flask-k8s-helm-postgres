# reactdo

[reactdo](https://www.reactdo.org) is a standards-compliant, simple to use wiki optimized for creating documentation. It is targeted at developer teams, workgroups, and small companies. All data is stored in plain text files, so no database is required.

## TL;DR;

```console
$ helm install stable/reactdo
```

## Introduction

This chart bootstraps a [reactdo](https://github.com/bitnami/bitnami-docker-reactdo) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters. This chart has been tested to work with NGINX Ingress, cert-manager, fluentd and Prometheus on top of the [BKPR](https://kubeprod.io/).

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release stable/reactdo
```

The command deploys reactdo on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the reactdo chart and their default values.

|              Parameter               |               Description                                  |                   Default                     |
|--------------------------------------|------------------------------------------------------------|-----------------------------------------------|
| `global.imageRegistry`               | Global Docker image registry                               | `nil`                                         |
| `global.imagePullSecrets`            | Global Docker registry secret names as an array            | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`                     | Global storage class for dynamic provisioning                                               | `nil`                                                        |
| `image.registry`                     | reactdo image registry                                    | `docker.io`                                   |
| `image.repository`                   | reactdo image name                                        | `bitnami/reactdo`                            |
| `image.tag`                          | reactdo image tag                                         | `{TAG_NAME}`                                  |
| `image.pullPolicy`                   | Image pull policy                                          | `Always`                                      |
| `image.pullSecrets`                  | Specify docker-registry secret names as an array           | `[]` (does not add image pull secrets to deployed pods) |
| `nameOverride`                       | String to partially override reactdo.fullname template with a string (will prepend the release name) | `nil` |
| `fullnameOverride`                   | String to fully override reactdo.fullname template with a string                                     | `nil` |
| `reactdoUsername`                   | User of the application                                    | `user`                                        |
| `reactdoFullName`                   | User's full name                                           | `User Name`                                   |
| `reactdoPassword`                   | Application password                                       | _random 10 character alphanumeric string_     |
| `reactdoEmail`                      | User email                                                 | `user@example.com`                            |
| `reactdoWikiName`                   | Wiki name                                                  | `My Wiki`                                     |
| `service.type`                       | Kubernetes Service type                                    | `LoadBalancer`                                |
| `service.port`                       | Service HTTP port                                          | `80`                                          |
| `service.httpsPort`                  | Service HTTPS port                                         | `443`                                         |
| `service.loadBalancerIP`             | Kubernetes LoadBalancerIP to request                       | `nil`                                         |
| `service.externalTrafficPolicy`      | Enable client source IP preservation                       | `Cluster`                                     |
| `service.nodePorts.http`             | Kubernetes http node port                                  | `""`                                          |
| `service.nodePorts.https`            | Kubernetes https node port                                 | `""`                                          |
| `ingress.enabled`                    | Enable ingress controller resource                         | `false`                                       |
| `ingress.hosts[0].name`              | Hostname to your reactdo installation                     | `reactdo.local`                              |
| `ingress.hosts[0].path`              | Path within the url structure                              | `/`                                           |
| `ingress.hosts[0].tls`               | Utilize TLS backend in ingress                             | `false`                                       |
| `ingress.hosts[0].certManager`       | Add annotations for cert-manager                           | `false`                                       |
| `ingress.hosts[0].tlsSecret`         | TLS Secret (certificates)                                  | `reactdo.local-tls`                          |
| `ingress.hosts[0].annotations`       | Annotations for this host's ingress record                 | `[]`                                          |
| `ingress.secrets[0].name`            | TLS Secret Name                                            | `nil`                                         |
| `ingress.secrets[0].certificate`     | TLS Secret Certificate                                     | `nil`                                         |
| `ingress.secrets[0].key`             | TLS Secret Key                                             | `nil`                                         |
| `persistence.enabled`                | Enable persistence using PVC                               | `true`                                        |
| `persistence.reactdo.storageClass`  | PVC Storage Class for reactdo volume                      | `nil` (uses alpha storage class annotation)   |
| `persistence.reactdo.accessMode`    | PVC Access Mode for reactdo volume                        | `ReadWriteOnce`                               |
| `persistence.reactdo.size`          | PVC Storage Request for reactdo volume                    | `8Gi`                                         |
| `resources`                          | CPU/Memory resource requests/limits                        |  Memory: `512Mi`, CPU: `300m`                 |
| `livenessProbe.enabled`              | Enable/disable the liveness probe                          | `true`                                        |
| `livenessProbe.initialDelaySeconds`  | Delay before liveness probe is initiated                   | 120                                           |
| `livenessProbe.periodSeconds`        | How often to perform the probe                             | 10                                            |
| `livenessProbe.timeoutSeconds`       | When the probe times out                                   | 5                                             |
| `livenessProbe.failureThreshold`     | Minimum consecutive failures to be considered failed       | 6                                             |
| `livenessProbe.successThreshold`     | Minimum consecutive successes to be considered successful  | 1                                             |
| `readinessProbe.enabled`             | Enable/disable the readiness probe                         | `true`                                        |
| `readinessProbe.initialDelaySeconds` | Delay before readinessProbe is initiated                   | 30                                            |
| `readinessProbe.periodSeconds   `    | How often to perform the probe                             | 10                                            |
| `readinessProbe.timeoutSeconds`      | When the probe times out                                   | 5                                             |
| `readinessProbe.failureThreshold`    | Minimum consecutive failures to be considered failed       | 6                                             |
| `readinessProbe.successThreshold`    | Minimum consecutive successes to be considered successful  | 1                                             |
| `nodeSelector`                       | Node labels for pod assignment                             | `{}`                                          |
| `affinity`                           | Affinity settings for pod assignment                       | `{}`                                          |
| `tolerations`                        | Toleration labels for pod assignment                       | `[]`                                          |
| `podAnnotations`                     | Pod annotations                                            | `{}`                                          |
| `metrics.enabled`                    | Start a side-car prometheus exporter                       | `false`                                       |
| `metrics.image.registry`             | Apache exporter image registry                             | `docker.io`                                   |
| `metrics.image.repository`           | Apache exporter image name                                 | `bitnami/apache-exporter`                     |
| `metrics.image.tag`                  | Apache exporter image tag                                  | `{TAG_NAME}`                                  |
| `metrics.image.pullPolicy`           | Image pull policy                                          | `IfNotPresent`                                |
| `metrics.image.pullSecrets`          | Specify docker-registry secret names as an array           | `[]` (does not add image pull secrets to deployed pods)      |
| `metrics.podAnnotations`             | Additional annotations for Metrics exporter pod            | `{prometheus.io/scrape: "true", prometheus.io/port: "9117"}` |
| `metrics.resources`                  | Exporter resource requests/limit                           | {}                                            |

The above parameters map to the env variables defined in [bitnami/reactdo](http://github.com/bitnami/bitnami-docker-reactdo). For more information please refer to the [bitnami/reactdo](http://github.com/bitnami/bitnami-docker-reactdo) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set reactdoUsername=admin,reactdoPassword=password \
    stable/reactdo
```

The above command sets the reactdo administrator account username and password to `admin` and `password` respectively.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml stable/reactdo
```

> **Tip**: You can use the default [values.yaml](values.yaml)

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

## Persistence

The [Bitnami reactdo](https://github.com/bitnami/bitnami-docker-reactdo) image stores the reactdo data and configurations at the `/bitnami/reactdo` path of the container.

Persistent Volume Claims are used to keep the data across deployments. There is a [known issue](https://github.com/kubernetes/kubernetes/issues/39178) in Kubernetes Clusters with EBS in different availability zones. Ensure your cluster is configured properly to create Volumes in the same availability zone where the nodes are running. Kuberentes 1.12 solved this issue with the [Volume Binding Mode](https://kubernetes.io/docs/concepts/storage/storage-classes/#volume-binding-mode).

See the [Configuration](#configuration) section to configure the PVC or to disable persistence.

## Upgrading

### To 3.0.0

Backwards compatibility is not guaranteed unless you modify the labels used on the chart's deployments.
Use the workaround below to upgrade from versions previous to 3.0.0. The following example assumes that the release name is reactdo:

```console
$ kubectl patch deployment reactdo-reactdo --type=json -p='[{"op": "remove", "path": "/spec/selector/matchLabels/chart"}]'
```
