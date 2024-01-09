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

## Reference
* [Add GPU nodes to your cluster](https://googlecloudplatform.github.io/kubeflow-gke-docs/dev/docs/customizing/#add-gpu-nodes-to-your-cluster)