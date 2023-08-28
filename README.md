# RKE2 cluster template

This project contains rke2 cluster template helm chart, which can be applied with values.yaml as configurations to create clusters.

### How to use

The general cluster configuration options are available through [values.yaml](./charts/values.yaml).

```yaml
# cluster specific values
cluster:
  # specify cluster name
  name: cluster-example

  # specify cluster labels
  labels: {}

  # specify cluster annotations
  annotations: {}

# specify cloud credential secret name, do not need to be provided if using custom driver
cloudCredentialSecretName: example

# specify cloud provider, options are amazonec2, digitalocean, azure, vsphere or custom
cloudprovider: ""

# enable network policy
enableNetworkPolicy: false

kubernetesVersion: "v1.21.0-alpha2+rke2r1"

# specify extra env variables in cluster-agent deployment
# agentEnvs:
#  - name: HTTP_PROXY
#     value: foo.bar

# general RKE options
rke:
  # worker configuration settings
  workerConfig:
  - config:
      # Node name
      # node-name: ""
      # Disable embedded containerd and use alternative CRI implementation
      # container-runtime-endpoint: ""
      # Override default containerd snapshotter (default: "overlayfs")
      # snapshotter: ""
      # IP address to advertise for node
      # node-ip: "1.1.1.1"
      # Kubelet resolv.conf file
      # resolv-conf: ""
      # Customized flag for kubelet process
      # kubelet-arg: ""
      # Customized flag for kube-proxy process
      # kube-proxy-arg: ""
      # Kernel tuning behavior. If set, error if kernel tunables are different than kubelet defaults. (default: false)
      # protect-kernel-defaults: false
      # Enable SELinux in containerd (default: false)
      # selinux: true
      # Cloud provider name
      # cloud-provider-name: ""
      # Cloud provider configuration file path
      # cloud-provider-config: ""
    machineLabelSelector:
      matchLabels:
        foo: bar

  # enable local auth endpoint
  localClusterAuthEndpoint:
    enabled: false
  # specify fqdn of local access endpoint
  # fqdn: foo.bar.example
  # specify cacert of local access endpoint
  # caCerts: ""

  # Specify upgrade options
  upgradeStrategy:
    controlPlaneDrainOptions:
      enabled: false
      # deleteEmptyDirData: false
      # disableEviction: false
      # gracePeriod: 0
      # ignoreErrors: false
      # skipWaitForDeleteTimeoutSeconds: 0
      # timeout: 0
    workerDrainOptions:
      enabled: false
      # deleteEmptyDirData: false
      # disableEviction: false
      # gracePeriod: 0
      # ignoreErrors: false
      # skipWaitForDeleteTimeoutSeconds: 0
      # timeout: 0
    workerConcurrency: "1"
```

To provide your own configuration, modify the original values.yaml and create your own version, and pass it to helm. For example:

```bash
helm install --namespace fleet-default --values ./charts/your-own-values.yaml do-cluster ./charts
```

For different cloud provider options on nodepools, checkout

[Amazonec2](./charts/values-aws.yaml)

[DigitalOcean](./charts/values-do.yaml)

[Harvester](./charts/values-harvester.yaml)

[Vsphere](./charts/values-vsphere.yaml)

[Azure](./charts/values-azure.yaml)

### Version control

The version control is implemented as helm release history and can easily be implemented by UI to provide operation history and rollback.

# License

Copyright (c) 2014-2021 [Rancher Labs, Inc.](http://rancher.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
