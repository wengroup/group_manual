(label:fireworks)=

# Fireworks

[Fireworks](https://materialsproject.github.io/fireworks) enables easy managing and executing workflows.

## Installing

Let's first clone the `fireworks` repo into the `~/Packages` directory, and then install it in the `ht_mat` conda environment.

```bash
$ mkdir -p ~/Packages && cd ~/Packages
$ git clone https://github.com/mjwen/fireworks.git
$ conda activate ht_mat
$ pip install -e fireworks
```

Note, here we clone from the `https://github.com/mjwen/fireworks.git` repo, not the official repo, because we need to use the `uri_mode` for MongoDB Atlas URI. Once [this PR](https://github.com/materialsproject/fireworks/pull/494) is merged, we can use the official repo.

## Configuration

Fireworks needs to be configured before it can work properly. For each of the file below, create it the `<CONFIG_DIR>` directory and put in the corresponding content. You will need to replace `<CONFIG_DIR>` by the full path to your config file directory, everything else in `<>` by your [MongoDB credentials](label:database).

```{note}
See [Atomate2 Workflows](label:atomate2) for what your `<CONFIG_DIR>` is.
```

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

### my_launchpad.yaml

This file specifies the database to store Fireworks lanuchpad info, and other launchpad settings.

```yaml
host: mongodb+srv://<mongo_username>:<mongo_password>@serverlessinstance0.nisxfj9.mongodb.net/?retryWrites=true&w=majority
name: <database>
uri_mode: true
logdir: null
Istrm_lvl: DEBUG
user_indices: []
wf_user_indices: []
```

### my_qadapter.yaml

This file specifics how to run a job using the SLURM scheduler. You may want to adjust a few stuff (e.g. `walltime`, `ntasks`, `mem`, `pre_rocket` e.t.c.) to suit your needs.

```yaml
_fw_name: CommonAdapter
_fw_q_type: SLURM
rocket_launch: rlaunch singleshot
nodes: 1
ntasks: 24
walltime: 0-00:30:00
account: wen
job_name: fw_job
# mem: 50GB
signal: SIGINT@60
pre_rocket: |
  module load vasp-wen/6.3.2
  conda activate ht_mat
```

## Running a flow

## More information

atomate2 documentation: https://materialsproject.github.io/atomate2/
