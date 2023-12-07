# Data/ML Operation on Google Cloud Platform

End-to-end, spanning from the ETL pipeline to the machine learning model development pipeline, all built upon Google Cloud Platform resources

## Description

This GitHub repository focuses on Data Operations using Apache Airflow for diverse data sources. The processed and tuned data is stored in Google Cloud's BigQuery for Data Warehouse capabilities or Google Cloud Storage for Data Lake purposes. Furthermore, the repository integrates Machine Learning operations using Kubeflow, deployed on Google Kubernetes Engine (GKE). The GKE setup includes Nvidia GPU nodes, providing support for CUDA for deep learning development. Additionally, the system incorporates Ray Cluster to enhance scalability and parallelism in distributed computing. To deploy and host models on the Google Cloud Platform, the workflow utilizes Google Cloud's Vertex AI, ensuring a comprehensive and scalable solution for data and machine learning workflows.

## High-Level Architecture Diagram
### Data Operation
![DataOps](./images/dataops-flowchart.jpg)

## License

This project is licensed under the MIT License - see the LICENSE file for details