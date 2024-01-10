# Extra configuration for Kubeflow

## Adding GPU node to the GKE cluster

1. Use `containerpool-gpu.yaml` file
    - Chnage these values:
        * KF_NAME: Kubeflow name
        * KF_PROJECT: Project name
        * LOCATION: Location
    - You can also change the GPU type if you want:
        `gcloud compute accelerator-types list`
2. Apply the node pool patch file using kubectl command:  
    `kubectl --context="${MGMTCTXT}" --namespace="${KF_PROJECT}" apply -f <path-to-gpu-nodepool-file>`
3. After adding GPU to the Kubeflow cluster, run the following command to install NVIDIA drivers:  
    `kubectl --context="${KF_NAME}" apply -f https://raw.githubusercontent.com/googlecloudplatform/container-engine-accelerators/master/nvidia-driver-installer/cos/daemonset-preloaded.yaml`

## Adding TPU node to the GKE cluster

- In `<YOUR_KF_DIRECTORY>/common/cluster/upstream/cluster.yaml` file, you have to set this value:
    * `enableTpu: true``
    * This should be done when you are creating GKE cluster because `enableTpu` is immutable once cluster is created
    * File should look like this: 
    ```yaml
    apiVersion: container.cnrm.cloud.google.com/v1beta1
    kind: ContainerCluster
    ...
    spec:
    ...
    enableTpu: true
    networkingMode: VPC_NATIVE
    networkRef:
        name: containercluster-dep-vpcnative
    subnetworkRef:
        name: containercluster-dep-vpcnative
    ipAllocationPolicy:
        servicesSecondaryRangeName: servicesrange
        clusterSecondaryRangeName: clusterrange
    ...
    ...
    ---
    apiVersion: compute.cnrm.cloud.google.com/v1beta1
    kind: ComputeNetwork
    metadata:
    name: containercluster-dep-vpcnative
    spec:
    routingMode: REGIONAL
    autoCreateSubnetworks: false
    ---
    apiVersion: compute.cnrm.cloud.google.com/v1beta1
    kind: ComputeSubnetwork
    metadata:
    name: containercluster-dep-vpcnative
    spec:
    ipCidrRange: 10.2.0.0/16
    region: us-west1
    networkRef:
        name: containercluster-dep-vpcnative
    secondaryIpRange:
    - rangeName: servicesrange
        ipCidrRange: 10.3.0.0/16
    - rangeName: clusterrange
        ipCidrRange: 10.4.0.0/16
    ```
## Reference
* [Customize Kubeflow on Google Cloud](https://googlecloudplatform.github.io/kubeflow-gke-docs/dev/docs/customizing/)