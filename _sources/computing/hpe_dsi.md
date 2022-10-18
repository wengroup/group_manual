# HPE DSI

This guide walks through the basics on using the HPE Data Science Institute clusters 
at UH.

## Get an account

If you have never used HPE DSI clusters, first request an account at https://uh.edu/rcdc/getting-started/request-account.php. The below information may be needed:

- Principal Investigator's (PI): Mingjian Wen
- PI Email address: mjwen@uh.edu
- Grant information: N/A
- Please select the Resource (Cluster): Carya
- Please select your login shell: Bash

You will receive an email shortly after submitting your request, which contains the login information such as your `username` (called `Login name` in the email).

## Log into the system

You need to use `ssh` to log into the cluster.
In any terminal on Linux or Mac ([Linux subsystem](https://docs.microsoft.com/en-us/windows/wsl/) can be installed on Windows), type

```
$ ssh <username>@carya.rcdc.uh.edu
```

Replace `<username>` by your username from the email and then press `Enter`. Next, provide your `CougarNet` credentials.

**Note**, the cluster can only be accessed via the UH campus network (wired or UHSecure/eduroam wireless). If you are not connecting from it, you need to use the [UH VPN](https://uh.edu/infotech/services/computing/networks/vpn/).

## Submit jobs

- Do not submit jobs from your home directory `/home/<username>`, which is not configured for I/O and has a limited storage space of 10GB.
- Do not submit jobs on the login node; it can affect other users.

Instead, submit jobs to the compute node from the project directory and using [Slurm](https://slurm.schedmd.com) script.

First, create a directory with your `username`:

```
$ cd /project/wen
$ mkdir <username>      # change <username> to yours
$ chmod g-w <username>  # remove write access for others
```

All your jobs should be submitted in the `project/wen/<username>` directory and its subdirectories.

Next, let's submit a job. Suppose you want to run a python script `example.py` placed in `project/wen/<username>`. A Slurm script for it can be:

```bash
#!/bin/bash -l

#SBATCH --job-name=my_1st_job
#SBATCH --account=wen           # account of our group
#SBATCH --time=00:10:00         # run for a max of 10 mins
#SBATCH --nodes=1               # run on 1 node

python example.py
```

Copy the above content into a file named, e.g., `submit.sh`, and place it in the same directory as `example.py`. Then you can submit the job using `sbatch`:

```
$ sbatch submit.sh
```

## Using GPU

```bash
#!/bin/bash -l

#SBATCH --job-name=my_1st_job
#SBATCH --account=wen
#SBATCH --time=00:10:00
#SBATCH --nodes=1
#SBATCH --mem=10GB  # don't forget this; otherwise, it can throw out-of-memory error
#SBATCH --gpus=1    # run on 1 gpu

python example.py
```

## Check balance

To check the group allocations and accounts, use

```
$ sbalance
```

## More information

Submitting job: https://uh.edu/rcdc/support-services/user-guide/getting-started-clusters

Open a ticket at the HPE DSI Support Center: https://support.hpedsi.uh.edu

Policies and data management: https://hpedsi.uh.edu/about/policies
