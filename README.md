## Technical How to's

This repository hosts the technical blogs for Oracle for Research.

#### [Quick Oracle Cloud links for researchers](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/Important%20Links.md)
---

### Getting started
1. [Getting started with your Oracle cloud tenancy](https://blogs.oracle.com/oracle-for-research/oracle-cloud-fundamentals-for-researchers%3a-getting-started-with-your-cloud-tenancy)
2. [Moving data to an Oracle cloud Instance](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/MovingDataToOracleCloud.md)
3. [Important considerations for setting up and Oracle cloud instance](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/Important%20Considerations.md)
5. [Mounting shared block storage in a cluster](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/Mounting%20shared%20block%20storage.md)
6. [SSH options for cloud access (upcoming)]
7. [Setting up User Configuration and Organization structure](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/Setting-up-an=Org-structure.md)
7. [Identity federation and options (upcoming)]

### Architecture and automation
1. [Standard Architecture](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/StandardArchitecture.md)
2. [Cloud Bursting Architecture](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/CloudBursting.md)
3. [Automation setup through Terraform Stacks](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/AutomationSetup.md)
4. [Automation with OCI Command line interface](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/OCI-CLI.md)
5. [Kubernetes IaaS on GPU clusters](https://github.com/rghosh9/Technical-HowTo-s/blob/main/k8s-on-oci.md)
5. [Choosing the right data science platform (upcoming)]

### Performance and benchmarks 
1. [**Molecular dynamics GPU Benchmarking with NAMD 3alpha (DRAFT)**](https://github.com/rghosh9/Technical-HowTo-s/blob/main/MDPerformanceTesting.md)
2. [Benchmarks with OCI shapes](https://github.com/OracleForResearch/Technology-How-Tos/blob/main/BenchmarkingWithShapes.md)
2. [NVIDIA A100 Performance on Oracle cloud](https://blogs.oracle.com/cloud-infrastructure/nvidia-a100-bare-metal-performance-in-oracle-cloud-infrastructure)
3. [HPC Performance on Intel on Oracle Cloud](https://blogs.oracle.com/cloud-infrastructure/optimize-your-high-performance-computing-with-oracle-cloud-on-intel)
4. [Monitoring Tools (upcoming)](https://github.com/rghosh9/Technical-HowTo-s/blob/main/MonitoringTools.md)

### Technical Resources and Repo's

Follow these links to get up and running:

#### 1. Filesystems

* [GlusterFS:](https://github.com/oci-hpc/oci-hpc-gluster) Launch a Gluster filesystem on OCI.
* [BeeGFS](https://github.com/oracle-quickstart/oci-beegfs-beeond-rdma) Deploy BeeGFS on RDMA clustered network with local NVMe.
* [Spectrum Scale:](https://github.com/oracle-quickstart/oci-ibm-spectrum-scale) Launch a Gluster filesystem on OCI.
* [Lustre Filesystem:](https://github.com/oracle-quickstart/oci-lustre) Deploy Lustre parallel distributed file system on OCI.
* [NFS Filesystem:](https://github.com/oracle-quickstart/oci-nfs) Terraform scripts to deploy active/passive Network File System.

#### 2. Application Images

* [Gromacs on GPU:](https://github.com/oci-hpc/oci-hpc-runbook-gromacs) Runbook to deploy Gromacs on OCI GPUs and run a benchmark. 
* [NAMD Runbook](https://github.com/oci-hpc/oci-hpc-runbook-namd) Deploy NAMD on GPU servers.
* [Jupyter GPU Server:](https://github.com/oracle-quickstart/oci-gpu-jupyter) Jupyter notebook server deployed on GPU. 
* [Oracle ML in Autonomous DB](https://github.com/oracle-quickstart/oci-arch-data-science) Deploy autonomous database and train your machine learning models in the database where you data already lives. 

#### 3. Cluster Management

* [Quick Start Starter Kit](https://github.com/oci-hpc/hpc-starter-kit) Get started with this HPC lab.
* [Quick Start HPC:](https://github.com/oracle-quickstart/oci-hpc) deploy a HPC clusters via terraform.
* [Deploy Slurm](https://github.com/oracle-quickstart/oci-slurm) Deploy Slurm compute cluster on OCI. 
* [Cluster Network](https://github.com/oci-hpc/oci-hpc-clusternetwork) Cluster networking in OCI. 
* [Cluster in the Cloud:](https://cluster-in-the-cloud.readthedocs.io/en/latest/oracle-infrastructure.html) Setup and deploy clusters, developed on OCI by Bristol University Advanced Computing Lab.

#### 4. Data Management

* [Kafka Data Stream](https://github.com/oracle-quickstart/oci-kafka) Deploy Kafka for real time data pipelines and streaming. 
