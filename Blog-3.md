Important Considerations for setting up an Oracle Cloud Instance

By Rajib Ghosh, Senior Solutions Architect, Oracle for Research

Understanding the basics of setting up an Oracle Cloud tenancy and
instance can help researchers and the technology specialists get running
quickly. However, taking a moment to understand some additional details
can help optimize your use of Oracle Cloud. We encourage you to consider
the following points when setting up an Oracle cloud instance

A compute instance can be virtual machine (VM) or a physical bare metal
machine (BM). Here, we explain the key considerations for setting up a
compute instance.

-   Compute images

-   Instance shapes

-   Network tiers and security lists

-   Usage control, automation and credits

**Compute images**

A compute image is a template of a virtual hard drive that determines
the operating system and other software for an instance. Oracle cloud
provides the following types of images - 

1.  [Platform images]{.ul} -- These are pre-built Linux or Windows
    operating system images ready to be deployed in the Oracle cloud.
    Platform images are tested by Oracle against various hardware shapes
    and are optimized to perform on Oracle cloud. Each image comes with
    multiple release builds to choose from. This is available as
    advanced option for compute instance creation. Platform image for
    [ARM based
    devices](https://archlinuxarm.org/#:~:text=Our%20collaboration%20with%20Arch%20Linux,and%20responsibility%20over%20the%20system.)
    is available through Oracle Linux 8 image.

![9d0ace8d437771d0ab7defbb12129a9d](media/image1.jpeg){width="0.2076388888888889in"
height="0.2076388888888889in"} Choose pre-built platform images while
starting your project. If you software configurations are not closely
tied to a Linux distribution like Centos or Ubuntu, we recommend using
Oracle Linux. This has certain maintenance, security and compatibility
advantages such as automated patching over other releases on Oracle
cloud. You can convert your current Linux distributions to Oracle Linux
quickly with [this link](https://linux.oracle.com/switch/centos/). Also,
note that windows images cannot be exported out of the Oracle cloud
tenancy because of Microsoft licensing considerations and you may need
to take a backup of your installed software and data and export them
out.

2.  [Oracle images]{.ul} -- These are pre-built images created by Oracle
    with software tools pre-installed in them. They are tested for
    software version compatibilities against the OS version and are
    installed with latest patches. They are also tested against relevant
    sample data. They are designed to jump-start research projects and
    deliver a common image framework for researchers within and across
    universities. Some of the popular HPC (High performance computing)
    and Data science images are listed below:

    1.  [AI (All-in-One) GPU Image for Data
        Science](https://console.us-ashburn-1.oraclecloud.com/marketplace/application/78643201/usageInformation)

    2.  [Genome analysis
        toolkit](https://console.us-ashburn-1.oraclecloud.com/marketplace/application/81390072/usageInformation)

    3.  [Julia AI/HPC GPU
        Image](https://console.us-ashburn-1.oraclecloud.com/marketplace/application/79537675/usageInformation)

    4.  [NVIDIA images and NVIDIA GPU
        image](https://console.us-ashburn-1.oraclecloud.com/marketplace/application/54854361/usageInformation)

![9d0ace8d437771d0ab7defbb12129a9d](media/image1.jpeg){width="0.2076388888888889in"
height="0.2076388888888889in"} You may use the following steps to
determine whether you need to use an Oracle provided image or build your
own from scratch.

a.  Compare the toolset and the version provided by Oracle image with
    the toolsets and version you require. Oracle images usually provides
    latest compatible working software versions with patches applied.
    Also, Oracle images are tested and benchmarked against relevant
    shapes with representative sample data. Check to see if this is
    advantageous and works for your scenario.

b.  If the tools and versions required are very specific and have a much
    lesser footprint than the Oracle image, it is better to start from
    the closest operating system image.

c.  Consult with Oracle for Research or Oracle cloud technical team for
    a solution that works best for your scenario.

```{=html}
<!-- -->
```
3.  [Cloud marketplace images]{.ul} - These are [Oracle cloud partner
    images](https://cloudmarketplace.oracle.com/marketplace/en_US/productHomePage)
    developed by various third party vendors. These images can be
    directly provisioned to your Oracle cloud tenancy from the
    marketplace without any download. Some marketplace images of
    interest to researchers are included below --

    1.  [Oracle HPC
        Cluster](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/67628143)
        and [Oracle HPC File
        system](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/75560175)

    2.  [NVIDIA GPU Cloud machine
        image](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/54854361)

    3.  [Oracle Linux 7 Cluster Networking
        Image](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/63394796)

    4.  Molecular dynamics images ( [NAMD
        runbook](https://github.com/oci-hpc/oci-hpc-runbook-namd) and
        [GROMACS
        runbooks](https://github.com/oci-hpc/oci-hpc-runbook-gromacs)) 

    5.  [Oracle marketplace slurm image (HPC + Slurm
        combo)](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/67628143)

    6.  [Oracle cloud slurm
        image](https://github.com/oracle-quickstart/oci-slurm)

    7.  [BeeGFS on
        demand](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/81525078)

![C:\\9d0ace8d437771d0ab7defbb12129a9d](media/image1.jpeg){width="0.20902777777777778in"
height="0.20902777777777778in"} Consider testing with these images if
you are looking to build [cluster networking
infrastructure](https://cloudmarketplace.oracle.com/marketplace/en_US/listing/73328167)
using Lustre or BeeGFS

4.  [Github Images]{.ul} -- Images with associated code and
    documentation are also provided in [OCI-HPC
    Github](https://github.com/oci-hpc). OCI images are also available
    as containers and can be found in [opencontainers
    Github](https://github.com/opencontainers/image-spec) repository.
    The github repositories can be cloned or forked by you for
    additional customization and provides a more collaborative and
    community development approach.

5.  [Custom images]{.ul} -- These are images you create from on-campus
    or from a different cloud. They contain with your custom tools and
    versions, configurations and data. Once uploaded they can be shared
    within Oracle cloud across tenancies and exported out for external
    usage as well. You can also build them from a running Oracle cloud
    instance as well. Custom images provide a point-in-time snapshot of
    an instance and can be versioned.

![9d0ace8d437771d0ab7defbb12129a9d](media/image1.jpeg){width="0.2076388888888889in"
height="0.2076388888888889in"} Use custom images to build the same
instance in another availability domain. Export the image to object
store and download it to move it out of Oracle cloud. You can also [move
attached block
volumes](https://blog.hussaindba.com/export-import-custom-image-copying-backup-of-block-volumes-between-the-regions-in-oci/)
as well using between OCI tenancies and regions

6.  [Boot volumes]{.ul} -- are a persistent way to keep your software
    installs and configurations in a volume to use in another instance
    later. Boot volumes cannot be shared by multiple instances
    concurrently and can be used within the same availability domain in
    your tenancy. However, they can be cloned to replicate and build
    another instance. Boot volumes can be extended as well.

7.  [Image OCIDs]{.ul} -- are the unique identity tags allocated to an
    image in Oracle cloud. It is possible to have multiple OCID for an
    image based on various regions i,e Ashburn, Frankfurt. You may also
    share OCID for custom images you built with other researchers as
    well. For more information, you may refer to [Oracle cloud provided
    images](https://docs.cloud.oracle.com/en-us/iaas/images/) or [Oracle
    custom
    images](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/managingcustomimages.htm)

![9d0ace8d437771d0ab7defbb12129a9d](media/image1.jpeg){width="0.2076388888888889in"
height="0.2076388888888889in"}Use Image OCID feature to manage and share
resources in an environment with large number of cloud images with many
researchers working simultaneously.

**Instance shapes**

Instance shapes are hardware specifications (i,e CPU, memory or storage)
that can be used to spin up a hardware instance of a specific image.
Instance shapes are broadly categorized as virtual (VM) or physical bare
metal (BM) and are available from multiple vendors. Instance shapes
provides you with the flexibility to scale your application across low
cost to high performance hardware available in the cloud. Oracle cloud
provides both flexible (AMD Rome) and fixed shapes (Intel Skylake).

The following table describes the available shapes, specification and
their usage.

+-------------+-------------+-------------+-------------+-------------+
| **Instance  | **Shape     | **Shape**   | **Spec      | ![9d0a      |
| type**      | Series**    |             | ification** | ce8d437771d |
|             |             |             |             | 0ab7defbb12 |
|             |             |             |             | 129a9d](med |
|             |             |             |             | ia/image1.j |
|             |             |             |             | peg){width= |
|             |             |             |             | "0.20763888 |
|             |             |             |             | 88888889in" |
|             |             |             |             | height="    |
|             |             |             |             | 0.207638888 |
|             |             |             |             | 8888889in"} |
|             |             |             |             | **Features, |
|             |             |             |             | Tips and    |
|             |             |             |             | Additional  |
|             |             |             |             | links**     |
+=============+=============+=============+=============+=============+
| Virtual     | AMD Rome    | Flexible    | oCPU 0\~64  | Better      |
|             |             | oCPU        |             | price-      |
|             |             |             | Memory      | p           |
|             |             | VM.Stan     | 0\~1TB      | erformance. |
|             |             | dardE3.Flex |             |             |
|             |             |             | Block       | *Start with |
|             |             |             | storage     | smaller and |
|             |             |             | only        | scale your  |
|             |             |             |             | workload    |
|             |             |             | *(Memory    | with to a   |
|             |             |             | and network | larger oCPU |
|             |             |             | bandwidth   | shape to    |
|             |             |             | scales      | benchmark   |
|             |             |             | linearly    | on          |
|             |             |             | with oCPU)* | price-p     |
|             |             |             |             | erformance. |
|             |             |             |             | [Oracle     |
|             |             |             |             | blog on AMD |
|             |             |             |             | ROME        |
|             |             |             |             | shape       |
|             |             |             |             | s](https:// |
|             |             |             |             | blogs.oracl |
|             |             |             |             | e.com/cloud |
|             |             |             |             | -infrastruc |
|             |             |             |             | ture/announ |
|             |             |             |             | cing-the-la |
|             |             |             |             | unch-of-e3- |
|             |             |             |             | standard-in |
|             |             |             |             | stance-on-a |
|             |             |             |             | md-rome-arc |
|             |             |             |             | hitecture)* |
+-------------+-------------+-------------+-------------+-------------+
|             | Intel       | Fixed oCPU  | oCPU :      | *Mostly for |
|             | Skylake     |             | 1\~24       | general     |
|             |             |   VM.       |             | purpose     |
|             |             | Standard2.1 | Memory :    | workloads   |
|             |             |   ------    | 15\~320GB   | i.e running |
|             |             | ----------- |             | an          |
|             |             |   VM.       | Network :   | a           |
|             |             | Standard2.2 | 1\~24Gbps   | pplication. |
|             |             |   VM.       |             | Better      |
|             |             | Standard2.4 | Block       | price       |
|             |             |   VM.       | storage     | performance |
|             |             | Standard2.8 | only        | for         |
|             |             |   VM.S      |             | c           |
|             |             | tandard2.16 | *(Memory    | ontinuously |
|             |             |   VM.S      | and network | running     |
|             |             | tandard2.24 | band width  | VMs. Can be |
|             |             |             | scales      | shut down   |
|             |             |             | linearly    | and brought |
|             |             |             | with oCPU)* | back up as  |
|             |             |             |             | standard    |
|             |             |             |             | shapes are  |
|             |             |             |             | not billed  |
|             |             |             |             | in stopped  |
|             |             |             |             | state.*     |
+-------------+-------------+-------------+-------------+-------------+
|             | Legacy and  | Always free | 1 oCPU+1GB  | *Use for    |
|             | Specialty   | shape       | RAM         | Oracle      |
|             | shapes      |             |             | cloud       |
|             |             | VM.Standa   | Block       | automation  |
|             |             | rdE2.1Micro | storage (1  | and         |
|             |             |             | x 46GB)     | scheduling  |
|             |             |             |             | scripts.    |
|             |             |             | *Can run    | You may     |
|             |             |             | c           | also use    |
|             |             |             | ontinuously | this as a   |
|             |             |             | with no     | secure      |
|             |             |             | billing.    | gateway VM  |
|             |             |             | Only 2 per  | to your     |
|             |             |             | tenancy is  | compute VMs |
|             |             |             | allowed.*   | and         |
|             |             |             |             | clusters in |
|             |             |             |             | a private   |
|             |             |             |             | subnet.*    |
+-------------+-------------+-------------+-------------+-------------+
|             | Legacy and  | Standard    | oCPU :1\~8  | *Better     |
|             | Specialty   | AMD shapes  |             | price-      |
|             | shapes      |             | Memory :    | performance |
|             |             |   VM.S      | 1\~64 GB    | than VM     |
|             |             | tandardE2.1 |             | standard    |
|             |             |   ------    | Network :   | shapes*.    |
|             |             | ----------- | 0.          | *Good for   |
|             |             |   VM.S      | 48\~5.6Gbps | general and |
|             |             | tandardE2.2 |             | low CPU     |
|             |             |   VM.S      | Block       | test        |
|             |             | tandardE2.4 | storage     | workloads   |
|             |             |   VM.S      | only        | in a        |
|             |             | tandardE2.8 |             | virtual     |
|             |             |             | *(High      | en          |
|             |             |             | performant  | vironment.* |
|             |             |             | AMD EPYC    |             |
|             |             |             | shapes with |             |
|             |             |             | linear      |             |
|             |             |             | scaling of  |             |
|             |             |             | memory and  |             |
|             |             |             | network     |             |
|             |             |             | capacity    |             |
|             |             |             | with oCPU)* |             |
+-------------+-------------+-------------+-------------+-------------+
|             | Legacy and  | DenseIO     | oCPU :      | *Faster IO  |
|             | Specialty   | shapes      | 8\~24       | p           |
|             | shapes      |             |             | erformance. |
|             |             |   VM        | Memory :    | Recommended |
|             |             | .DenseIO2.8 | 120\~320GB  | for testing |
|             |             |   -----     |             | IO          |
|             |             | ----------- | Storage :   | intensive   |
|             |             |   VM.       | 6.4\~25.6   | workloads   |
|             |             | DenseIO2.16 | NVMe SSD    | on a VM     |
|             |             |   VM.       | storage     | based NVME  |
|             |             | DenseIO2.24 | with        | environment |
|             |             |             | 1\~4drives  | before      |
|             |             |             |             | scaling up  |
|             |             |             | *(Memory    | to          |
|             |             |             | and storage | co          |
|             |             |             | scales      | rresponding |
|             |             |             | linearly    | BM shapes*  |
|             |             |             | with oCPU)* |             |
+-------------+-------------+-------------+-------------+-------------+
|             | Legacy and  | GPU shapes  | oCPU : 12   | *Only       |
|             | Specialty   |             |             | available   |
|             | shapes      | VM.GPU2.1   | Memory : 72 | VM GPU      |
|             |             |             | GB          | shape. Test |
|             |             |             |             | your AI/ML  |
|             |             |             | Block       | GPU         |
|             |             |             | storage     | workload in |
|             |             |             | only        | a VM based  |
|             |             |             |             | GPU         |
|             |             |             |             | environment |
|             |             |             |             | before      |
|             |             |             |             | scaling to  |
|             |             |             |             | BM GPU      |
|             |             |             |             | shape*      |
+-------------+-------------+-------------+-------------+-------------+
| Bare metal  | Physical    | Standard    | oCPU : 52   | *Price      |
|             | server      | shapes      | Memory :    | -performant |
|             |             |             | 768GB       | bare metal  |
|             |             |   -------   |             | shape. Test |
|             |             | ----------- | Network :   | your        |
|             |             |   BM.St     | 2NIC x 25   | workloads   |
|             |             | andardE2.52 | Gbps        | before      |
|             |             |   -------   |             | moving to   |
|             |             | ----------- | Block       | the BM2.52  |
|             |             |             | storage     | DenseIO     |
|             |             |             | only        | shape*      |
+-------------+-------------+-------------+-------------+-------------+
|             |             | DenseIO     | oCPU : 52   | *Highest IO |
|             |             | shapes      | Memory :    | intensive   |
|             |             |             | 768GB       | p           |
|             |             |   ------    |             | erformance. |
|             |             | ----------- | Network :   | Additional  |
|             |             |   BM.D      | 2NIC x      | block       |
|             |             | enseIOE2.52 | 25Gbps      | storages    |
|             |             |   ------    |             | (up to 1PB  |
|             |             | ----------- | 51.2 TB     | / instance) |
|             |             |             | local NVME  | can be      |
|             |             |             | SSD         | attached as |
|             |             |             |             | well.       |
|             |             |             |             | Scaling     |
|             |             |             |             | flexibility |
|             |             |             |             | by          |
|             |             |             |             | clustering  |
|             |             |             |             | as well as  |
|             |             |             |             | attached    |
|             |             |             |             | block       |
|             |             |             |             | volumes*    |
+-------------+-------------+-------------+-------------+-------------+
|             |             | Standard    | oCPU : 64   | *Price      |
|             |             | shapes      | Memory 512  | -performant |
|             |             |             |             | for high    |
|             |             |   BM.St     | Network :   | CPU / lower |
|             |             | andardE2.64 | 2NIC x      | memory and  |
|             |             |   -------   | 25Gbps      | IO          |
|             |             | ----------- |             | workloads   |
|             |             |             | Block       | than BM2.52 |
|             |             |             | storage     | shapes. A   |
|             |             |             | only        | good start  |
|             |             |             |             | to test     |
|             |             |             |             | your        |
|             |             |             |             | workload on |
|             |             |             |             | BM shapes*  |
+-------------+-------------+-------------+-------------+-------------+
|             |             | Standard    | oCPU : 128  | *Highest    |
|             |             | shapes      | Memory 2048 | oCPU,       |
|             |             |             |             | memory and  |
|             |             |   BM.Sta    | Network :   | bandwidth   |
|             |             | ndardE3.128 | 2NIC x      | for large   |
|             |             |   --------  | 50Gbps      | IO          |
|             |             | ----------- |             | throughputs |
|             |             |             | Block       | over block  |
|             |             |             | storage     | storage.    |
|             |             |             | only        | Test your   |
|             |             |             |             | workload    |
|             |             |             |             | for         |
|             |             |             |             | comparable  |
|             |             |             |             | price       |
|             |             |             |             | performance |
|             |             |             |             | against     |
|             |             |             |             | BM.DenseIO  |
|             |             |             |             | 2.52        |
|             |             |             |             | shapes*     |
+-------------+-------------+-------------+-------------+-------------+
|             |             | GPU shapes  | oCPU 28     | *Bare metal |
|             |             |             | Memory 256  | 3.x GPU     |
|             |             | +-          | GB          | shapes are  |
|             |             | ----------+ |             | based on    |
|             |             | |           | oCPU 52     | nVIDIA V100 |
|             |             | BM.GPU2.2 | | Memory 768  | as opposed  |
|             |             | |           | GB          | to older    |
|             |             |           | |             | P100        |
|             |             | |           | Network     | ar          |
|             |             | BM GPU3.4 | | 2NIC x      | chitecture. |
|             |             | |           | 25Gbps      | Suited for  |
|             |             |           | |             | Deep        |
|             |             | |           | Block       | learning    |
|             |             | BM.GPU3.8 | | storage     | (DL) GPU    |
|             |             | +-          | only        | ap          |
|             |             | ----------+ |             | plications. |
|             |             |             |             | DL          |
|             |             |             |             | a           |
|             |             |             |             | pplications |
|             |             |             |             | with large  |
|             |             |             |             | matrix      |
|             |             |             |             | ma          |
|             |             |             |             | nipulations |
|             |             |             |             | can take    |
|             |             |             |             | advantage   |
|             |             |             |             | of BM 3.x   |
|             |             |             |             | (higher     |
|             |             |             |             | tensor      |
|             |             |             |             | core)       |
|             |             |             |             | shapes*     |
+-------------+-------------+-------------+-------------+-------------+
|             |             | HPC shapes  | oCPU 36     | *           |
|             |             |             | Memory 384  | Recommended |
|             |             |   -         |             | for         |
|             |             | ----------- | 6.7 local   | parallel    |
|             |             |             | NVME (8     | workloads   |
|             |             |  BM.HPC2.36 | drives)     | where       |
|             |             |   -         |             | in          |
|             |             | ----------- | Network     | ter-process |
|             |             |             | 2NIC x      | co          |
|             |             |             | 25Gbps +    | mmunication |
|             |             |             | 100Gbps     | is          |
|             |             |             | RDMA        | predominant |
|             |             |             |             | So scaling  |
|             |             |             |             | requires a  |
|             |             |             |             | RDMA        |
|             |             |             |             | cluster     |
|             |             |             |             | networking  |
|             |             |             |             | to          |
|             |             |             |             | facilitate  |
|             |             |             |             | inter-node  |
|             |             |             |             | com         |
|             |             |             |             | munication* |
+-------------+-------------+-------------+-------------+-------------+
|             |             | Old         | oCPU 36     | *This may   |
|             |             | standard    | memory      | be used for |
|             |             | shapes      | 256GB       | workloads   |
|             |             |             |             | with lower  |
|             |             | BM.S        | oCPU 44     | CPU or      |
|             |             | tandard1.36 | memory      | memory      |
|             |             |             | 512GB       | r           |
|             |             | BM.St       |             | equirements |
|             |             | andardB.144 | Network     | and lower   |
|             |             |             | 1NIC x      | throughput  |
|             |             |             | 25Gbps      | r           |
|             |             |             |             | equirements |
|             |             |             | Block       | or when the |
|             |             |             | storage     | high end    |
|             |             |             | only        | shapes are  |
|             |             |             |             | not         |
|             |             |             |             | available*  |
+-------------+-------------+-------------+-------------+-------------+

**Network tier and security lists**

Network components like subnets and security lists provide the required
isolation to your VM/BM instances from direct external access. Oracle
cloud network is restrictive by default and only allows SSH (port 22)
access to allow external logins to the VMs. This is sufficient for most
researcher use-cases if you perform your work logging into the VMs.
However, if you wish to stand up an application and have specific port
requirements, you need to open them by adding a ingress security list
entry for the VMs subnet.

The diagram below shows addition of port 3389 to enable RDP access for
any Windows VMs in the subnet. Note that the source is set to a CIDR
value 0.0.0.0/0 meaning that is open to anyone trying to RDP to Oracle
cloud on that port. However, you may consult your on-campus network
administrator to set this your on-campus network CIDR values to restrict
access to your cloud VM to university network only.

![](media/image2.png){width="6.5in" height="3.5444444444444443in"}

However, you may also secure your VM in a self-service manner without
the help of your network administrator. However, it is a bit involved
and a recommended practice is to create all your computational VM/BM in
a private subnet and access them from a free tier windows or Linux
machine in a public facing subnet in Oracle cloud. This lets you SSH
connect to your Always free VM in public subnet and use it as a gateway
to connect to your compute instances in the private subnet. You may
refer to [OCI VCN Introductory
page](https://www.oracle.com/a/ocom/docs/cloud/virtual-cloud-network-100.pdf)
or consult OFR technical team for details. A schematic diagram of the
architecture and a screenshot showing the updated security list rule are
shown below. This security rule will only allow RDP (remote desktop)
access from the Oracle cloud free tier VM as opposed to anywhere in the
internet

![](media/image3.png){width="5.25in" height="3.5416666666666665in"}

![](media/image4.png){width="6.5in" height="0.5638888888888889in"}

1.  Managing usage and costs - 

**Usage control, automation and credits**

To get more out of Oracle cloud tenancy credits, it is imperative that
compute resources be fully utilized. With most of HPC and AI/ML
computations being batch oriented, it is extremely important that
instances be used at full or near full capacity and terminated when not
in use. Credit control can be effectively performed in two ways -- 1)
Using high-end shapes only for computational cycles 2) Using automation
to start / terminate instances when not in use. You may refer to
[Resource billing for stopped
instances](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/restartinginstance.htm#resource-billing)
for more details as well.

![9d0ace8d437771d0ab7defbb12129a9d](media/image1.jpeg){width="0.2076388888888889in"
height="0.2076388888888889in"}Some of the important tips are described
below:

1.  [Start with low-cost and scale to high-end shapes]{.ul} -- Standard
    > and AMD VM shapes provides lower per hour cost and is recommended
    > to use during the software installation, image building and
    > testing phases for your project. Standard shapes can be stopped
    > without billing but high end shapes like DenseIO, GPU or HPC
    > shapes must be terminated to stop billing. It is recommended to
    > get a benchmark of your workload by starting with a VM and slowly
    > moving to expensive BM shapes.

2.  [Start with low data volume and scale up]{.ul}-- Start with a lower
    > data volume to get a sense of CPU and memory utilization and scale
    > the data to find the optimal threshold of CPU and RAM for that
    > shape. You may do the same for IO intensive loads to check out
    > various storage types (local SSD, block volume or a combination)
    > to see how they perform while scaling with data. Testing workloads
    > in this way can give you a sense of performance gains that can be
    > achieved as you scale up your workloads and shape.

3.  [Utilizing GPU/HPC shapes]{.ul} -- GPU and HPC shapes are expensive
    > and should only be used during computational cycles only. The BM
    > GPU and HPC shapes are billed by the hour and hence need previous
    > workload cycle estimation for effective usage. Measuring CPU and
    > memory utilization at the operating system level and CPU/GPU level
    > and benchmarking them against your data can help. Several tools
    > like (free,vmstat or iostat),
    > [fio](https://fio.readthedocs.io/en/latest/fio_doc.html),
    > [mdtest](https://wiki.lustre.org/MDTest), IO500 or
    > [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface)
    > can be used for this purpose.

4.  [Instance creation and termination automation]{.ul} -- The rule of
    > thumb is to create an instance just before your computation and
    > terminate them after your run. You may also do this manually from
    > OCI console but it is easier said than done and hence automation
    > is a better choice. Oracle recommends OCI command line
    > interface (CLI) or Terraform scripts in conjunction with Linux
    > shell or Windows powershell for automation and control. Though OCI
    > provides an application API interface, OCI CLI provides a quicker
    > and efficient way to develop and manage automation. The following
    > links can help you on your journey to automation:

```{=html}
<!-- -->
```
a.  [OCI CLI Getting
    started](https://oracle.github.io/learning-library/oci-library/DevOps/OCI_CLI/OCI_CLI_HOL.html#practice-5-use-query-to-find-oracle-linux-image-id,-then-launch-a-compute-instance)
    and
    [documentation](https://docs.cloud.oracle.com/en-us/iaas/Content/API/Concepts/cliconcepts.htm)

b.  [OCI CLI github site](https://github.com/oracle/oci-cli)

c.  [OCI CLI command
    reference](https://docs.cloud.oracle.com/en-us/iaas/tools/oci-cli/2.12.11/oci_cli_docs/)

d.  [OCI terraform provider
    examples](https://github.com/terraform-providers/terraform-provider-oci/tree/master/examples)

e.  [Cluster in the
    cloud](https://cluster-in-the-cloud.readthedocs.io/en/latest/)

```{=html}
<!-- -->
```
5.  [Estimating cluster size and instance scaling]{.ul} -- Estimate the
    > number of nodes for a specific shape is necessary for optimal use
    > of the Oracle cloud shapes and clusters. Though the estimation
    > process can vary depending on project needs, a general practice is
    > to estimate the total CPU/GPU hours, IO throughput and network
    > bandwidth for the project, benchmark it against the Oracle cloud
    > shapes to estimate the number of nodes required for your workload.
    > Once done, you may be able to use the OCI [Instance
    > pooling](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/creatinginstancepool.htm)
    > feature to
    > [auto-scale](https://docs.cloud.oracle.com/en-us/iaas/Content/Compute/Tasks/autoscalinginstancepools.htm)
    > nodes based on your workload.

6.  [Credit control with cost analysis, budgeting and alerts]{.ul} --
    > [Cost
    > analysis](https://docs.cloud.oracle.com/en-us/iaas/Content/Billing/Concepts/costanalysisoverview.htm)
    > provides you with a summarized and a drill down view of resource
    > usage and costs for your tenancy with a variety of visualization
    > charts. You can also customize them by adding different filters
    > that may be of importance to you. Oracle cloud automatically
    > generates detail summarized reports and you may be able to
    > integrate them with your on-campus cost reporting system as well.
    > Furthermore, it is possible to set soft limits on your tenancy
    > spend
    > ([budgets](https://docs.cloud.oracle.com/en-us/iaas/Content/Billing/Concepts/budgetsoverview.htm))
    > and [set
    > alerts](https://docs.cloud.oracle.com/en-us/iaas/Content/Billing/Tasks/managingalertrules.htm)
    > to know when you are exceeding your budgets.
