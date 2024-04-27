Introduction
------------

The River Computing (RC) is the SLURM based cluster that allows for mainly bioinformatics usages.
It utilizes the `nextflow` bioinformatics workflow manager to run bioinformatics pipelines using executor `slurm`.
Slurm allows to allocate the resource of CPU cores, memory, and GPUs efficiently.


The cluster is designed to run bioinformatics pipelines in a scalable and efficient manner. Minimal 
installization to the cluster is required to run bioinformatics pipelines, includes the installation of the container
engine `singularity` , `micromamba`, `docker-rootless-extras`.


For storage, the cluster allows to use `goofys` to mount the S3 bucket to the cluster. The S3 bucket is mounted to the
approriate directory. The S3 bucket can be used to storage the input data, output data, and the reference data. For other
storage options, `rclone` can be used to mount the cloud storage to the cluster.


Special thanks to the contributors for this documentations that allows the bioinformatican to use the cluster efficiently.

**Contributors:**
- [Thanh-Giang Tan Nguyen](https://www.linkedin.com/in/thanh-giang-tan-nguyen-761b28190/)

