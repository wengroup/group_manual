(label:conda)=

# Conda Environment

Frequently we need a specific configuration and package versions for one project, which can conflict with another project's needs. [Conda environment](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html) is a great way to manage packages and versions. It allows us to create a separate environment where we can install any package versions for one project without affecting anything outside of this environment.

## Installation

::::{tab-set}

:::{tab-item} On macOS

Conda is not installed on macOS by default. To install it, first do

```shell
curl https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o conda_installer.sh

bash conda_installer.sh
```

Then follow the instructions on your screen, basically:

```
Are sure you want to continue the installation? [yes|no]
[no] >>> yes  # type yes and then press Enter

Do you accept the license terms? [yes|no]
[no] >>> yes  # type yes and then press Enter

Miniconda3 will now be installed into this location:
/Users/<username>/miniconda3
...
# press Enter

Do you wish the installer to initialize Miniconda3
by running conda init? [yes|no]
[yes] >>> yes  # type yes and then press Enter
```

This will install conda to your home directory `~/miniconda3`.
To confirm it's successfully installed, do `$ conda --version` , and you will see something like `conda 4.14.0`.

```{note}
This works for Apple M1 chip. For more installing options (e.g. for Intel chip), see the [miniconda doc](https://docs.conda.io/en/latest/miniconda.html).
```

:::

:::{tab-item} On HPE DSI clusters

On the HPE DSI clusters (e.g. carya and sabine), `conda` is already installed, but it is not on `PATH` by default. When you run `$ conda`, you will get an error like `-bash: conda: command not found`.

To get it on `PATH`, do:

```shell
module load python
```

```{tip}
You can add the above line to your `~/.bashrc`. Then it will be automatically loaded each time you login to the cluster, avoid executing it manually.
```

:::
::::

## Creating a conda environment

Once conda is installed, create a new environment using the below command. In this example, we create an environment named `my_env` (you can create multiple environments with different names).

```shell
conda create --name my_env
```

## Using a conda environment

To use the `my_env` conda environment, first activate it by:

```shell
conda activate my_env
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

```shell
conda init bash
source ~/.bashrc
```

Note, you just need to run the above two commands once; it will modify the `~/.bashrc` file to automatically configure for later usage.

### Installing packages

Then, you can install packages into this environment. In this example, we install Python version 3.10

```shell
conda install python=3.10
```

### Listing packages in your environment

```shell
conda list
```

### Listing available environment

If you have created multiple environments, you can get a list of them by:

```shell
conda env list
```

## Mamba (optional)

Conda is great, but it can be slow. For example, it can take a long time to download the packages. To get around this, we can use [mamba](https://github.com/mamba-org/mamba), a reimplementation of the conda package manager with running speed taken into consideration.

### Installing mamba

Once you have activated your conda environment, e.g. `conda activate my_env`, you can install mamba into the `my_env` environment via conda

```shell
conda install -c conda-forge mamba
```

```{note}
We add the `-c conda-forge` to install the `mamba` packages from the `conda-forge` channel instead of the `main` channel. For more information of channels, see the [documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/channels.html).
```

### Using mamba

You can use `mamba` to do pretty much everything that `conda` can do by replacing the `conda` command by the `mamba` command. For example, you can install `pymatgen` via

```shell
mamba install -c conda-forge pymatgen
```

## Changing default conda settings (optional)

```{warning}
This is not needed on your Mac; skip it.

This is optional on HPE DSI clusters, but it is good to do it.
```

### Changing environment directory

By default, if we create a new environment, it will be stored in the `$HOME` directory (e.g. `/home/<username>/.conda/envs`).
Conda environments can sometimes get quite big, but each of us only has a quota of 10G for `$HOME`. This can easily lead to out-of-quota problem. We can change the default environment directory to avoid this.

You should have access to our group project directory, i.e. `/project/wen`, which has a much larger disk quota. We will configure conda to store environments there.

First, create a directory under your username.

```shell
cd /project/wen
mkdir <username>   # change <username> to your HPE DSI user name
```

**Note**, all `<username>` below needs to be changed to yours.

Within your directory, create a directory to store conda environment. In this example, we create a directory `/home/wen/<username>/conda/envs`) to store the environments:

```shell
cd <username>
mkdir conda && mkdir conda/envs
```

Then, config conda to prepend to `envs_dirs` the directory we've just created:

```shell
conda config --prepend envs_dirs /project/wen/<username>/conda/envs
```

This is all you need to do. To ensure it's successful, let's check it by

```shell
conda config --show
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

### Changing package directory

Similarly, by default, when you install a package, it will first be downloaded to a place in your `$HOME`, i.e. `/home/<username>/.conda/pkgs`). You can change the default package storage directory as well to avoid out-of-quota problems.

```shell
conda config --prepend pkgs_dirs /tmp
```

In this case, we set it to the `/tmp` directory to avoid using our group project space.

Of course, you can use `conda config --show` or view `~/.condarc` to see the changes.
