(label:hpe:dsi)=

# HPE DSI

This page describes the basics of using the HPE Data Science Institute clusters at UH.

typo-WF

typo-EO

typo-DG


## Getting an account

If you have never used HPE DSI clusters, first request an account at https://uh.edu/rcdc/getting-started/request-account.php. The below information may be needed:

- Principal Investigator (PI): Mingjian Wen
- PI Email address: mjwen@uh.edu
- Grant information: N/A
- Please select the Resource (Cluster): Carya
- Please select your login shell: Bash

You will receive an email shortly after submitting your request, which contains the login information such as your `username` (called `Login name` in the email).

## Logging into the system

You need to use `ssh` to log into the cluster.
In any terminal on Linux or Mac ([Linux subsystem](https://docs.microsoft.com/en-us/windows/wsl/) can be installed on Windows), type

```
$ ssh <username>@carya.rcdc.uh.edu
```

Replace `<username>` by yours, press `Enter` and then provide your CougarNet credentials to login.

```{tip}
The clusters can be accessed via the `UHSecure` not the `UHGuest` network. If you cannot log in and see error message like `ssh: connect to host carya.rcdc.uh.edu port 22: Operation timed out`, check your Wi-Fi connection.

If you are off campus, use UH [VPN](https://uh.edu/infotech/services/computing/networks/vpn/) to get access.
```

## Transferring data

Transfer a file from your laptop to Carya:

```
$ scp /local/path/my_file.txt <username>@carya.rcdc.uh.edu:/remote/path
```

Transfer a file from Carya to your laptop:

```
$ scp <username>@carya.rcdc.uh.edu:/remote/path/my_file.txt /local/path
```

Alternatively, if you prefer a graphical user interface or want to transfer a large amount of data, `globus` is a good option. See [HPE DSI User Guide](https://uh.edu/rcdc/support-services/user-guide/getting-started-clusters) for instructions. [TODO: add instructions here].

## Submitting jobs

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

## Checking balance

To check the group allocations and accounts, use

```
$ sbalance
```

## More information

HPE DSI User Guide: https://uh.edu/rcdc/support-services/user-guide/getting-started-clusters

Open a ticket at the HPE DSI Support Center: https://support.hpedsi.uh.edu

Policies and data management: https://hpedsi.uh.edu/about/policies
