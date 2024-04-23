RC Systems 
===========
Supports 2 paritions in slurm:
- **standard** is designed for standard Jobs
- **gpu** is designed for GPU Jobs
For details on the hardware and software available on the system, please see the sections below.
.. table:: 
		:widths: 5, 25, 15, 20, 20, 15
		
+------------+---------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------+--+--+--+--+--+--+
| Partitions | Descriptions                                                                    | Compute Nodes                                                  | Notes                     |  |  |  |  |  |  |
+============+=================================================================================+================================================================+===========================+==+==+==+==+==+==+
| standard   | Support normal analysis                                                         | worker-01: 88 CPUS 254 GB RAM, 1TB SSD, 10TB HDD, Quadro 4000  |                           |  |  |  |  |  |  |
+------------+---------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------+--+--+--+--+--+--+
| gpus       | Support GPUs required analysis, such as computer vision, large languages models | worker-02: NA                                                  | Not have money to buy yet |  |  |  |  |  |  |
+------------+---------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------+--+--+--+--+--+--+

Operating system
----------------
The RC systems use the Linux Operating System (specifically Ubuntu 20.04 LTS) which is commonly used in HPC. We do not have any HPC systems running Windows (or MacOS). If you are unfamiliar with using Linux, please consider:

- Finding introduction to Linux resources online (through Google/Bing/Yahoo etc).
- Working through our brief Introduction to Linux course.
- Attending our Introduction to ARC training course (this does not teach you how to use Linux but the examples will help you gain a greater understanding).

Capability cluster (rc)
------------------------

The capability system - cluster name rc - has a total of 88 core worker nodes.
Currently, the system has 1 worker node with the following specifications: 

All nodes have the following:
- 2x Intel Xeon E5-2696 V4 (2.20 GHz / 22 cores / 44 threads) Socket 2011-3 CPU. The Platinum 8628 is a 24 core 2.90GHz Cascade Lake CPU. Thus all nodes have 48 CPU cores per node.
- 254GB memory
- OS is Ubunutu Linux 20.04 LTS Scheduler is SLURM.

Login Node
-------
The login node is only for login, Intel® Core™ i5-3470 Processor with 4 CPUs and 8GB RAM, 500GB HDD. It is only for login.

Storage
-------
NFS: Allows to share storage between nodes using the local network.
+ NFS server: login nodes
+ NFS client: worker nodes
+ NAS supports but not have yet
S3 Compatible Storage: Allows to share storage between nodes or personal computer using the internet. Using goofys to mount S3 bucket to the local file system.
+ S3 FPT
+ S3 CMS
+ S3 Viettel
Others: Using rclone to mount other cloud storage to the local file system. However, it is not recommended to use this method because it is slow and unstable.
+ Google Drive
+ One Drive
+ Dropbox