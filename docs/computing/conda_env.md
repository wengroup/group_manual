# Conda Environment

Frequently we need a specific configuration and package versions for one project, which can conflict with another project's needs.
[Conda env](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) is a great way to manage packages and versions. It allows us to create a separate `environment` where we can install any package versions for one project without affecting anything outside of this environment.

## Add conda to PATH

By default, `conda` is not on [PATH](https://janelbrandon.medium.com/understanding-the-path-variable-6eae0936e976) of HPE DSI clusters. When you call `conda`, you 
will get an error like `-bash: conda: command not found`. Get it on PATH by:

```
$ module load python
```

**Note**, you can add the above line to your `~/.bashrc`. Then it will be automatically loaded each time you login to the cluster, and you will no longer need to execute it manually.

## Create a conda environment

To create a new conda environment, use the following commands. In this example, we create an environment named `my_env`.

```
$ conda create --name my_env
```

## Use the created conda environment

To use the `my_env` conda environment, we need to first activate it by:

```
$ conda activate my_env
```

When you run this for the first time, you may see something like

```
CommandNotFoundError: Your shell has not been properly configured to use 'conda activate'.
To initialize your shell, run

    $ conda init <SHELL_NAME>

Currently supported shells are:
  - bash
  - fish
  - tcsh
  - xonsh
  - zsh
  - powershell
```

Then, you need to do

```
$ conda init bash
$ source ~/.bashrc
```

Note, you just need to do this above two commands once; not needed the next time you login to the cluster.

- Install packages

Then, you can install packages into this environment. In this example, we install Python version 3.9.7.

```
$ conda install python=3.9.7
```

### List packages in your environment

```
$ conda list
```

### List available environment

If you have created multiple environments, you can get a list of them by:

```
$ conda env list
```

## Change default conda settings (optional)

By default, if we create a new environemnt, it will be stored in the `$HOME` directory (e.g. `/home/<username>/.conda/envs`).
Conda environments can sometimes get quite big, but each of us only has a quota of 10G for `$HOME`. This can easily lead to out-of-quota problem. We can change the default environment directory to avoid this.

You should have access to our group project directory, i.e. `/project/wen`, which has a much larger disk quota. We will configure conda to store environments there.

First, create a directory under your username,

```
$ cd /project/wen
$ mkdir <username>   # change <username> to your HPE DSI user name
```

**NOTE**, all `<username>` below needs to be changed to yours.

Within your directory, create a directory to store conda environment. In this example, we create a directory `/home/wen/<username>/conda/envs`) to store the environments:

```
$ cd <username>
$ mkdir conda && mkdir conda/envs
```

Then, config conda to prepend to `envs_dirs` the directory we've just created:

```
$ conda config --prepend envs_dirs /project/wen/<username>/conda/envs
```

This is all you need to do. To ensure it's successful, let's check it by

```
$ conda config --show
```

This will generate a lot of output, but you will find something like:

```
envs_dirs:
  - /project/wen/<username>/conda/envs
  - /home/<username>/.conda/envs
  - /project/dsi/apps/python/3.9/envs
```

which means `/project/wen/<username>/conda/envs` is now configured as the default place to store your environments.

Alternatively, you can open `~/.condarc` to see all the changes you've made. You can even directly edit it to remove the changes or add new ones.

## Change package directory (Optional)

By default, when you install a package, it will first be downloaded to a place in your `$HOME`, i.e. `/home/<username>/.conda/pkgs`). You can change the default package storage directory as well to avoid out-of-quota problems.

```
$ conda config --prepend pkgs_dirs /tmp
```

In this case, we set it to the `/tmp` directory to avoid using our group project space.

Of course, you can use `conda config --show` or view `~/.condarc` to see the changes.

## Use mamba to accelerate conda (optional)

Conda is great, but it can be slow. For example, it can take a long time to download the
packages. To get around this, we can use [mamba](https://github.com/mamba-org/mamba),
which a reimplementation of the conda package manager with running speed taken into
consideration.

### Install mamba

Once you have activated your conda environment, e.g. `conda activate my_env`, you can install mamba into the `my_env` environment via conda

```
$ conda install -c conda-forge mamba
```

Note, we add the `-c conda-forge` to install the `mamba` packages from the `conda-forge` channel instead of the `main` channel. If you are interested, see the [documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html) to read more.

### Use mamba

You can use `mamba` to do pretty much everything that `conda` can do by replacing the `conda` command by the `mamba` command. For example, you can install `pymatgen` via

```
$ mamba install -c conda-forge pymatgen
```
