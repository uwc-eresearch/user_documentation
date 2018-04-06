# Submitting jobs to be run on the SANBI cluster

When running jobs on the SANBI cluster, you'll want to be logged into `queue00` as your SANBI user. From here you need to make a job file for the cluster scheduler in order to submit your jobs for processing. 

**DO NOT RUN JOBS DIRECTLY ON QUEUE00**.

## Creating the job file
You can copy the information below into a file with the name of your choice, normally ending in `.sh`. Edit all of the stuff inside of the \<\> brackets and remove the brackets.

```bash
#!/bin/bash

########################################################################
# Configuration for qsub.                                              #
# =======================                                              #
#                                                                      #
# This file is used to specify the arguments for the qsub program      #
# itself, as well as the program that you want to run on the cluster . #
#                                                                      #
# Jobs will automatically be assigned to machines in our cluster based #
# on how many resources you request.                                   #
#                                                                      #
########################################################################

# This is where you specify the flags that would be read by qsub,
# instead of you having to pass it in the command line. (e.g.
# instead of saying qsub -q long.q, you can use #$ -q long.q in here)

#$ -S /bin/bash
#$ -q <queuename>
#$ -N <jobname>
#$ -l h_vmem=<size>
#$ -l h_rt=<hh:mm:ss>
#$ -o <output_file_name>
#$ -e <error_file_name>

# This is the directory where you want to work from for your
# application (where your data is).
cd /where/ever/your/work/files/are

# Here you load the miniconda package to load bioconda packages
# OR you load the tool directly.
module load <packages you want>

# If you chose conda, you will load the conda tool using the
# below line.
<if you chose miniconda, you then use: source activate toolname here>

# Here you execute the tool and pass it arguments like you normally
#    would, assuming it is reading from the directory specified above.
<toolname> <tool flags/inputs>
```

If you don't use miniconda, then you will use `module load <software_name>`, followed by the `<toolname> <tool flags/inputs>` part, without specifying `source ...`.

You can get a list of modules, or tools, available on the cluster by running `module avail` on your queue00 account.

Your output log and error log files are normally generated in the directory that you run `qsub` from.

|Option|Description|
|-|-|
|-q queuename|The name of the queue you wish to run your job on.|
|-N jobname|The name of the job as reflected in `qstat`. **There must be NO spaces in the name**.|
|-l h_vmem=size|Maximum amount of memory required for job. E.g. '5G' would be 5GB|
|-l h_rt=hh:mm:ss|Maximum amount of time job may run for. hh = hours, mm = minutes, ss = seconds, e.g. 2h30m = 02:30:00|
|-o output_file_name|The name of the standard output log file generate.|
|-e error_file_name|The name of the standard error log file to generate.|
**Note that all \< and \> brackets are used to reference user supplied values and should not be included in the scripts.**

## Executing and managing jobs

In order to run a job, use the command `qsub` followed by your job file that you created with the adjusted info based on the above snippet. E.g:
```bash
qsub my_job_file.sh
```

When the job is running, you can use `qstat` to check your progress. You can also check the overall cluster usage by using `qstat -u '*'`. `qstat` will output something like the following:
```bash
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
7518386 0.75000 trimmomati eugene      r     04/06/2018 12:36:51 all.q@gridn1.sanbi.ac.za           1        
```

If you want ot stop a job, copy the `job-ID` for your respective job, and use it with `qdel`. E.g:
```bash
qdel 7575849
```
