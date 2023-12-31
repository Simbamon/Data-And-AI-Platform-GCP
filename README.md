# Data and AI Platform on Google Cloud Platform

End-to-end, spanning from the ETL pipeline to the machine learning model development pipeline, all built upon Google Cloud Platform resources

## Description

This GitHub repository focuses on Data Operations using Apache Airflow for diverse data sources. The processed and tuned data is stored in Google Cloud's BigQuery for Data Warehouse capabilities or Google Cloud Storage for Data Lake purposes. Furthermore, the repository integrates Machine Learning operations using Kubeflow, deployed on Google Kubernetes Engine (GKE). The GKE setup includes Nvidia GPU nodes, providing support for CUDA for deep learning development. Additionally, the system incorporates Ray Cluster to enhance scalability and parallelism in distributed computing. To deploy and host models on the Google Cloud Platform, the workflow utilizes Google Cloud's Vertex AI, ensuring a comprehensive and scalable solution for data and machine learning workflows.

## Getting Started

Following these instructions will help you set up and run a project for development and testing purposes. 

### Prerequisites

* Google Cloud Platform
* [Kubeflow](https://github.com/googlecloudplatform/kubeflow-distribution) on Google Kubernetes Engine
    - Kubeflow version: 1.7.0
    - Python version: 3.8.10
* Ray Cluster (w/KubeRay Operator)

### Installation

Below are step-by-step instructions on how to copy the sample notebook in Kubeflow JupyterLab and start exploring/developing

1. Make a new notebook in the Kubeflow
2. Clone the repo
   ```sh
   git clone https://github.com/Simbamon/Data-And-AI-Platform-GCP.git
   ```
3. Install packages in the notebook
   ```sh
   !pip install '<REQUIRED_PACKAGES_FOR_THE_NOTEBOOK>'
   ```

## High-Level Architecture Diagram
### Data Operation
![DataOps](./images/dataops-flowchart.jpg)

## License

This project is licensed under the MIT License - see the LICENSE file for details

## Reference

* Github [fast-neural-style-pytorch by rrmina](https://github.com/rrmina/fast-neural-style-pytorch)
* Github [vertex-ai-mlops by statmike](https://github.com/statmike/vertex-ai-mlops)
* Github [fcc-intro-to-llms by Infatoshi](https://github.com/Infatoshi/fcc-intro-to-llms)
* Github [RayTutorial by ClarityCoders](https://github.com/ClarityCoders/RayTutorial/tree/master)
* Blog [Saturn Cloud](https://saturncloud.io/blog/getting-started-with-ray-clusters/)

## Issues

* Fails to delploy Kubeflow with make-apply
   - Error: `parsing time "null" as "2006-01-02T15:04:05Z07:00": cannot parse "null" as "2006"`
   - Fix: Remove `creationTimestamp: null`
   ```
   # in "kubeflow-distribution/kubeflow/apps/profiles/upstream/crd/bases/kubeflow.org_profiles.yaml"
   apiVersion: apiextensions.k8s.io/v1
   kind: CustomResourceDefinition
   metadata: # kpt-merge: /profiles.kubeflow.org
   annotations:
   controller-gen.kubebuilder.io/version: v0.8.0
   internal.kpt.dev/upstream-identifier: 'apiextensions.k8s.io|CustomResourceDefinition|default|profiles.kubeflow.org'
   creationTimestamp: null # <- Remove this line
   name: profiles.kubeflow.org
   spec:
   ...
   ```
   - Reference bug in the [Github issue](https://github.com/kubeflow/kubeflow/issues/7041)
