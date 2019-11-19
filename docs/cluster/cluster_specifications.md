# Cluster Specifications

## Cluster Structure

The UWC Meerkat Cluster employs SLURM, an open source cluster management software. The cluster is structured with a head node (the login node), and several compute nodes. The head node is used for job submission and job managment. No software should be run on the head node. The compute nodes are used as worker nodes, where all software packages, scripts and pipelines are run. When submitting a job from the head node, the user will request resources required for the job and describe the task that is to be run. The SLURM manager will determine if the requested resources are available and assign a portion of a node or several nodes to the task - depending on the resources that were requested. The task will then be executed on the worker node(s). For more information about running or submitting a job, see [Running a job on the cluster](getting_started/submitting_jobs.md).

## Cluster Resource Specifications

A single `head node` exists with `6 CPUs` and `64GB RAM`. The head node has limited resources and should only be used for job submission and job managments.

`19 compute nodes` are available in the worker pool of the cluster. Each node has `48 CPUs` and `256GB RAM`. Note, these are the maximum specifications per node that can be requested when submitting a job.

The file system containers `24 x 6TB harddrives`, a total of roughly `138TB disk space` shared amongst all users. The disk space should be considered as `scratch` space, that is to say, temporary storage. Data and files should only be placed on disk during processing. The UWC Meerkat Cluster does not offer archiving or long term storage. No storage backup services exists on the cluster.
