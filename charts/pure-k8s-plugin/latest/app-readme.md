# pure-k8s-plugin
Pure Service Orchestrator Installation for Rancher Catalogs

### Configuration

The following table lists the configurable parameters and their default values.

|             Parameter       |            Description             |                    Default                |
|-----------------------------|------------------------------------|-------------------------------------------|
| `image.name`                | The image name       to pull from  | `purestorage/k8s`                         |
| `image.tag`                 | The image tag to pull              | `2.2.1`                                   |
| `image.pullPolicy`          | Image pull policy                  | `IfNotPresent`                            |
| `app.debug`                 | Enable/disable debug mode for app  | `false`                                   |
| `storageclass.isPureDefault`| Set `pure` storageclass to the default | `false`                               |
| `storageclass.pureBackend`  | Set `pure` storageclass' default backend type | `block`                               |
| `clusterrolebinding.serviceAccount.name`| Name of K8s/openshift service account for installing the plugin | `pure`                    |
| `flasharray.sanType`        | Block volume access protocol, either ISCSI or FC | `ISCSI`                     |
| `flasharray.defaultFSType`  | Block volume default filesystem type. *Not recommended to change!* | `xfs`     |
| `flasharray.defaultFSOpt`  | Block volume default mkfs options. *Not recommended to change!* | `-q`          |
| `flasharray.defaultMountOpt`  | Block volume default filesystem mount options. *Not recommended to change!* |     ""    |
| `flasharray.preemptAttachments`  | Enable/Disable attachment preemption! |     `true`    |
| `namespace.pure`            | Namespace for the backend storage  | `k8s`                                     |
| `orchestrator.name`         | Orchestrator type, such as openshift, k8s | `k8s`                              |
| `flexPath`                  | Full path of directory to install flex plugin, works with image.tag >= 2.0.1 | `/usr/libexec/kubernetes/kubelet-plugins/volume/exec` |
| *`arrays`                    | Array list of all the backend FlashArrays and FlashBlades | must be set by user, see an example below                |
| `nodeSelector`              | [NodeSelectors](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#nodeselector) | `{}` |
| `tolerations`               | [Tolerations](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/#concepts)  | `[]` |
| `affinity`                  | [Affinity](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity) | `{}` |

*Examples:
```yaml
arrays:
  FlashArrays:
    - MgmtEndPoint: "1.2.3.4"
      APIToken: "a526a4c6-18b0-a8c9-1afa-3499293574bb"
      Labels:
        rack: "22"
        env: "prod"
    - MgmtEndPoint: "1.2.3.5"
      APIToken: "b526a4c6-18b0-a8c9-1afa-3499293574bb"
  FlashBlades:
    - MgmtEndPoint: "1.2.3.6"
      APIToken: "T-c4925090-c9bf-4033-8537-d24ee5669135"
      NfsEndPoint: "1.2.3.7"
      Labels:
        rack: "7b"
        env: "dev"
    - MgmtEndPoint: "1.2.3.8"
      APIToken: "T-d4925090-c9bf-4033-8537-d24ee5669135"
      NfsEndPoint: "1.2.3.9"
      Labels:
        rack: "6a"
```

# License
https://www.purestorage.com/content/dam/purestorage/pdf/legal/pure-plugin-end-user-license-agmt-sept-18-2017.pdf
