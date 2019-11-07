# Meerkat Cluster Structure

The Meerkat cluster is a [SLURM](https://slurm.schedmd.com) cluster and includes a single head node and several compute or worker nodes. 

The head node is also the login in node, this is the node where a user lands when they ssh into the cluster. The head node is for job submission and job management. No code, software applications or processes should be run on the head node.

The compute nodes are where jobs are run, either through submitting a SLURM batch script, a script that describes the job to be executed, or by requesting time on a compute node and running software interactively.

Additional details about submitting or running jobs on the SLURM cluster can be found [here](getting_started/submitting_jobs.md).

## Slurm commands

Here are some useful Slurm commands:

| Command | Result                                                   |
| ------- | -------------------------------------------------------- |
| sinfo   | Shows information about the compute machines             |
| squeue  | Shows information about running jobs                     |
| sbatch  | Allows you to submit a job file or script to the cluster |
| scancel | Cancels a running job, provided a job ID                 |
| srun    | Run a single command without needing to provide a script |

You can find additional information about each command and what parameters can be supplied to the command using the `--help` or `-h` parameter, for example:

```
$ srun -h
```

This will list information and input parameters for the `srun` command.