# Submitting jobs to be run on the SANBI cluster

When running jobs on the SANBI cluster, you'll want to be logged into `queue` as your SANBI user. From here you need to make a job file, or script, for the cluster scheduler in order to submit your jobs for processing. 

## Preface

**!!! DO NOT RUN JOBS DIRECTLY ON QUEUE !!!**.

We try to ensure that everyone has a pleasant experience when using the cluster. There are some very powerful machines behind the headnode. If you run a job directly from the terminal while on `queue`, instead of providing a job script to the scheduler, you risk impacting the experience of other users as your job will be executing only on `queue` itself, instead of `queue` sending the job to one of the more powerful computers.

The scheduler system that we use at SANBI is called Slurm. It ensures that when you pass it a job file, or script, it will pass the work you intend to do to one or more of the machines that exist in our compute cluster that are intended to do the work.

## Slurm commands

| Command | Result |
| ------- | ------ |
| sinfo   | Shows information about the compute machines |
| squeue  | Shows information about running jobs |
| sbatch | Allows you to submit a job file or script to the cluster |
| scancel| Cancels a running job, provided a job ID |
| srun | Run a single command without needing to provide a script |

## Creating the job file
You can copy the information below into a file with the name of your choice, normally ending in `.sh`. Edit all of the stuff inside of the <\> brackets and remove the brackets.

```bash
#!/bin/bash

########################################################################
# Configuration for sbatch.                                            #
# =======================                                              #
#                                                                      #
# This file is used to specify the arguments for the sbatch program    #
# itself, as well as the program that you want to run on the cluster . #
#                                                                      #
# Jobs will automatically be assigned to machines in our cluster based #
# on how many resources you request.                                   #
#                                                                      #
########################################################################

#SBATCH --comment="This is a comment"                   # OPTIONAL: An arbitrary comment on the job
#SBATCH --job-name="This is the name of the job"        # REQUIRED: Give this job an arbitrary name
#SBATCH --output="%j.out"                               # REQUIRED: Direct STDOUT (normal output) here (file identifier),%j is substituted for the job number, keep this as is, but you can add to before it. E.g. "myjob.%j.out"
#SBATCH --error="%j.err"                                # REQUIRED: Direct STDERR (error output) here (file identifier), %j is substituted for the job number, keep this as is, but you can add to before it. E.g. "myjob.%j.err"
#SBATCH --time=01:00:00                                 # REQUIRED: Maximum time your job can run before it is force terminated. Hr:Min:Sec.
#SBATCH --mem=24G                                       # REQUIRED: Memory required for your job
#SBATCH --requeue                                       # OPTIONAL: On failure, requeue for another try
#SBATCH --verbose                                       # OPTIONAL: Increase informational messages
#SBATCH --export="SOMEVARIABLE=HELLO"                   # OPTIONAL: Set arbitrary environment variables

# Leave the following as is.
if [ x$SLURM_CPUS_PER_TASK == x ]; then
  export OMP_NUM_THREADS=8
else
  export OMP_NUM_THREADS=$SLURM_CPUS_PER_TASK
fi

# This is the directory where you want to work from for your
# application (where your data is).
cd /where/ever/your/work/files/are

# IF YOU WANT TO USE TOOLS PACKAGED AS SINGULARITY CONTAINERS:
# ============================================================
# A full example of running the fastqc tool would be something like:
# singularity exec /tools/containers/fastqc/fastqc-0.11.7.simg fastqc <input_data>
singularity exec /tools/containers/<tool_folder>/<tool_version>.simg <tool_executable> <tool input>

# IF YOU WANT TO USE YOUR OWN SCRIPTS OR TOOLS:
# =============================================
# You can copy your tool to queue and use it with your data through slurm.
# Assuming you're using a Python3 script:
python3 myscript.py <myscript.py input>
```

For now, to check which tools are available as containers, you can use:
```bash
edebeste@queue:~$ ls /tools/containers/
```
This will provide a list of containers. Feel free to request tools to be added to this if you require them by sending an email to help@sanbi.ac.za.

## Executing and managing jobs

In order to submit a script based on the template above, use the command `sbatch` followed by your job file that you created with the adjusted info based on the above snippet. E.g:
```bash
edebeste@queue:~$ sbatch my_job_file.sh
```

When the job is running, you can use `squeue` to check your progress. This will also show overall cluster usage. `squeue` will show output such as the following:
```bash
edebeste@queue:~$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
              1220      main bam2fast jgamield  R    8:12:51      1 cmc2-01-hpc.sanbi.ac.za
              1221      main    sleep edebeste  R       0:19      1 cmc2-04-hpc.sanbi.ac.za
```

You can also filter getting job information by users so that you don't get other people's jobs in the list. To do this you can use `squeue -u <username>`, for example: `squeue -u edebeste`.

If you want to stop a job, copy the `JOBID` for your respective job, and use it with `scancel`. E.g:
```bash
edebeste@queue:~$ scancel 1221
```

The following table summarizes the common statuses that you will see under the `ST` section in the `squeue` output:

| STATUS CODE | MEANING                             |
|:-----------:|-------------------------------------|
| R           | Job is running                      |
| S           | Job is allocated but suspended      |
| CD          | Job is in the process of completing |
| PD          | Job is waiting for free resources   |
| TO          | Job killed due to time limit        |
| F           | Job failed                          |
| OOM         | Job ran out of memory               |

More detail is available here: https://slurm.schedmd.com/squeue.html#SECTION_JOB-STATE-CODES

## Running interactive jobs

If you need to test a script or run a job that requires you to give it input, you can get access to one of the compute nodes through slurm by using the `srun` command as such:
```bash
edebeste@queue:~$ srun --mem=24G  --pty bash
```
This will give you access to a new shell which is logged into one of the powerful compute nodes:
```bash
edebeste@cmc2-01-hpc:~$ 
```
Here you can run a job or test or any other thing you need to interactively. Once you are done you can exit this session as normal using the command `exit`.