Overview
============

Introduction
------------

The River Computing (RC) is the SLURM based cluster that allows for mainly bioinformatics usages.
It utilizes the ``nextflow`` bioinformatics workflow manager to run bioinformatics pipelines using executor ``slurm``.
Slurm allows to allocate the resource of CPU cores, memory, and GPUs efficiently.


The cluster is designed to run bioinformatics pipelines in a scalable and efficient manner. Minimal 
installization to the cluster is required to run bioinformatics pipelines, includes the installation of the container
engine ``singularity`` , ``micromamba``, ``docker-rootless-extras``.


For storage, the cluster allows to use ``goofys`` to mount the S3 bucket to the cluster. The S3 bucket is mounted to the
approriate directory. The S3 bucket can be used to storage the input data, output data, and the reference data. For other
storage options, ``rclone`` can be used to mount the cloud storage to the cluster.

.. image:: images/slurm.svg
    :width: 800
    :alt:   starting Dolphin from the menu

Special thanks to the contributors for this documentations that allows the bioinformatican to use the cluster efficiently.

**Contributors:**

- `Thanh-Giang Tan Nguyen <https://www.linkedin.com/in/thanh-giang-tan-nguyen-761b28190/>`_


Hardwares and systems
---------------------
The ``login node`` is only for login, Intel® Core™ i5-3470 Processor with 4 CPUs and 8GB RAM, 500GB HDD. It is only for login.
For partitions, it included a group of workers (computing nodes) that has similar hardware and software configurations. For
example, the ``main`` partition is designed for standard Jobs, and the ``gpu`` partition is designed for GPU Jobs.

Supports 2 paritions in slurm:

- **main** is designed for standard Jobs

- **gpu** is designed for GPU Jobs

For details on the hardware and software available on the system, please see the sections below.

+------------+---------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------+
| Partitions | Descriptions                                                                    | Compute Nodes                                                  | Notes                     |
+============+=================================================================================+================================================================+===========================+
| main   | Support normal analysis                                                         | worker-01: 88 CPUS 254 GB RAM, 1TB SSD, 10TB HDD, Quadro 4000  |                           |
+------------+---------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------+
| gpu       | Support GPUs required analysis, such as computer vision, large languages models | worker-02: NA                                                  | NA |
+------------+---------------------------------------------------------------------------------+----------------------------------------------------------------+---------------------------+

Operating system
----------------
The RC systems use the Linux Operating System (specifically ``Ubuntu 20.04.05 LTS``) which is commonly used in HPC. We do not have any HPC systems running Windows (or MacOS). If you are unfamiliar with using Linux, please consider:

- Finding introduction to Linux resources online (through Google/Bing/Yahoo etc).
- Working through our brief Introduction to Linux course.
- Attending our Introduction to ARC training course (this does not teach you how to use Linux but the examples will help you gain a greater understanding).

Capability cluster (rc)
------------------------

The capability system - cluster name rc - has a total of 88 core worker nodes.
Currently, the system has 1 worker node with the following specifications: 

All nodes have the following:

- 2x Intel Xeon E5-2696 V4 (2.20 GHz / 22 cores / 44 threads) Socket 2011-3 CPU.
- 250GB memory
- OS is Ubunutu Linux 20.04 LTS Scheduler is SLURM.


Storage
-------
**NFS**: Allows to share storage between nodes using the local network area (LAN).

- NFS server: login nodes
- NFS client: worker nodes
- NAS supports but not have yet

By defaults, the <login nodes>:/home/ are mounted to the <worker nodes>:/home/ using NFS.
Therefore, the user can access the same home directory from any node within the cluster.
For example ``/home/giangnguyen`` on the login/controller node will be the same as ``/home/giangnguyen`` on the worker nodes.
For NFS based system (NAS), the mount point can be configured by the system administrator UI.

**S3 Compatible Storage**: 

Allows to share storage between nodes or personal computer using the internet. Using goofys to mount S3 bucket to the local file system.

- S3 AWS compatible storage: Minio, Ceph, CMC S3 distributed by `VNDATA <https://vndata.vn/>`_
- AWS S3: S3 storage

To mount the S3 bucket to the local file system, the user needs to install goofys and configure the S3 bucket.
The S3 bucket is mounted to the appropriate directory. The S3 bucket can be used to storage the input data, output data, and the reference data.
After adding the `s3 credentials <https://github.com/kahing/goofys>`_ , the user can mount the S3 bucket to the local file system by running the following command::
    
    goofys <s3_bucket_name>:<s3 path> --file-mode=0666 --dir-mode=0777 --endpoint=<your s3_url>



**Others**: Using rclone to mount other cloud storage to the local file system. However, it is not recommended to use this method because it is slow and unstable.
- Google Drive
- One Drive
- Dropbox