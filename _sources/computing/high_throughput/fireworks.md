(label:fireworks)=

# Fireworks

[Fireworks](https://materialsproject.github.io/fireworks) enables easy managing and executing workflows.

```{note}
The below instruction is for the `Carya` cluster. It may need slight adjustments for other clusters.
```

## Installing

After logging into the cluster, let's first clone the `fireworks` repo into the `~/Packages` directory, and then install it in the `ht_mat` conda environment.

```bash
$ mkdir -p ~/Packages && cd ~/Packages
$ git clone https://github.com/mjwen/fireworks.git
$ conda activate ht_mat
$ pip install -e fireworks
```

```{note}
See [Atomate2 Workflows](label:atomate2) for what `ht_mat` and `<CONFIG_DIR>` (to be used) are.
```

Here we clone from the `https://github.com/mjwen/fireworks.git` repo, not the official repo, because we need to use the `uri_mode` for MongoDB Atlas URI. Once [this PR](https://github.com/materialsproject/fireworks/pull/494) is merged, we can use the official repo.

## Configuration

Fireworks needs to be configured before it can work properly. For each of the yaml files below, create it in the `<CONFIG_DIR>` directory with the corresponding content. You will need to replace `<CONFIG_DIR>` by the full path to your config file directory, and everything else in `<>` by your [MongoDB credentials](label:database).

### FW_config.yaml

This file specifics fireworks configurations.

```yaml
CONFIG_FILE_DIR: <CONFIG_DIR>
QUEUE_UPDATE_INTERVAL: 5
```

Also, edit `~/.bashrc` and add:

```bash
export FW_CONFIG_FILE=<CONFIG_DIR>/FW_config.yaml
```

Don't forget to source it after editing, so that the modification will be effective in the current shell:

```bash
$ source ~/.bashrc
```

### my_launchpad.yaml

This file specifies the database to store Fireworks lanuchpad info, and other launchpad settings.

```yaml
host: <uri>
name: <database>
uri_mode: true
logdir: null
Istrm_lvl: DEBUG
user_indices: []
wf_user_indices: []
```

### my_qadapter.yaml

This file specifics how to run a job using the SLURM scheduler. You may want to adjust a few stuff (e.g. `walltime`, `ntasks`, `mem`, `pre_rocket` etc.) to suit your needs.

```yaml
_fw_name: CommonAdapter
_fw_q_type: SLURM
rocket_launch: rlaunch singleshot
nodes: 1
ntasks: 24
walltime: 0-01:00:00
account: wen
job_name: fw_job
# mem: 50GB
signal: SIGINT@60
pre_rocket: |
  module load vasp-wen/6.4.2
  conda activate ht_mat
```

## Running a flow

### Initializing launchpad

```{warning}
BE EXTREMELY CAREFUL WHEN RUNNING THIS RESET COMMAND. It will wipe all existing entries in your fireworks database in the fireworks, workflows, and launches collections.
```

```{warning}
You typically only need to run the reset command once. DON'T redo it unless you know what you are doing.
```

OK, let's state this again: BE EXTREMELY CAREFUL WHEN RUNNING THIS RESET COMMAND. It will wipe all existing entries in your fireworks database in the fireworks, workflows, and launches collections. Make sure the `ht_mat` conda environment is activated and then do `$ lpad reset` to initialize/reset your launchpad.

### Creating a workflow

Create a file named `example_flow.py` and put in it:

```python
from fireworks import LaunchPad
from atomate2.vasp.flows.core import RelaxBandStructureMaker
from jobflow.managers.fireworks import flow_to_workflow
from pymatgen.core import Structure

# construct a rock salt MgO structure
mgo_structure = Structure(
    lattice=[[0, 2.13, 2.13], [2.13, 0, 2.13], [2.13, 2.13, 0]],
    species=["Mg", "O"],
    coords=[[0, 0, 0], [0.5, 0.5, 0.5]],
)

# make a band structure flow to optimise the structure and obtain the band structure
bandstructure_flow = RelaxBandStructureMaker().make(mgo_structure)

# convert the flow to a fireworks WorkFlow object
wf = flow_to_workflow(bandstructure_flow)

# submit the workflow to the FireWorks launchpad
lpad = LaunchPad.auto_load()
lpad.add_wf(wf)
```

Then you can add it to your fireworks launchpad by `$ python example_flow.py`.

You can verify that it is added by:

```bash
lpad get_fws -s READY
```

### Launching a workflow

The above commands only add the workflow to the launchpad, but the workflow hasn't been submitted for running. To run the workflow, you can use the `qlaunch` command to submit jobs using SLURM. You can use `singleshot` to submit a single job or `rapidfire` to submit multiple jobs.

```{warning}
Make sure you are in the directory you want your calculations to be run from before running the below commands. On `Carya`, do not run the commands from your home directory, instead, create a directory (e.g. `fw_launches`) in `/project/wen/<your_carya_username>/` and run the commands from there.
```

::::{tab-set}

:::{tab-item} singleshot

```bash
$ conda activate ht_mat   # can be ignored if already activated
$ qlaunch singleshot
```

:::

:::{tab-item} rapidfire

```bash
$ conda activate ht_mat   # can be ignored if already activated
$ qlaunch rapidfire --nlaunches 1
```

You may want to increase the number of launches to submit more jobs.
Specifically, you can use `--nlaunches infinite` to keep submitting jobs without stop (use this mode with caution!).

:::
::::

```{note}
Use `$ qlaunch --help`, `$ qlaunch singleshot --help`, `$ qlaunch rapidfire --help` etc. to see help message on `qlaunch`.
```

### Monitoring your workflow

You can use appropriate SLURM commands, e.g. `squeue` to see whether your job starts or not.

Also, to check the status of your jobs, you can do

```bash
$ lpad get_fws -s RUNNING
```

Alternatively, you can use a Web GUI to monitor the status of your workflows. To enable this, follow the above `Installing` and `Configuration` steps to set it up on your laptop (not on the cluster). Then

```
$ lpad webgui  # on a local terminal not connected to the cluster
```

will open a tab in our web browser to show the status of your workflows.

## More information

- Fireworks documentation: https://materialsproject.github.io/fireworks
- Persson group handbook (note, this is for atomate1 workflow, but many things are the same for atomate2): https://materialsproject.gitbook.io/persson-group-handbook/computing/atomate-setup
