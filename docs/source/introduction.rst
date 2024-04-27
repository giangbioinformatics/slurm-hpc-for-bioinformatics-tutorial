Introduction
------------

The River Computing (RC) is the SLURM based cluster that allows for mainly bioinformatics usages.
It utilizes the `nextflow` bioinformatics workflow manager to run bioinformatics pipelines using executor `slurm`.
Slurm allows to allocate the resource of CPU cores, memory, and GPUs efficiently.

The cluster is designed to run bioinformatics pipelines in a scalable and efficient manner. Minimal 
installization to the cluster is required to run bioinformatics pipelines, includes the installation of the container
engine `singularity` , `micromamba`, `docker-rootless-extras`.