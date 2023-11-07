(label:atomate2)=

# Atomate2 Workflows

This guide discusses the steps to configure computational workflows on HPCs, mainly using [pymatgen](https://pymatgen.org), [jobflow](https://github.com/materialsproject/jobflow), [atomate2](https://materialsproject.github.io/atomate2/) and other related packages.

```{note}
The below instruction is for the HPE DSI `Carya` and `Sabine` cluster. It may need slight adjustments for other clusters.
```

```{note}
Make sure to have your [database credentials](label:database) ready before moving forward.
```

## Setting up a conda environment

Log into the cluster, and then create a conda environment:

```bash
$ conda create --name ht_mat
```

Activate the environment:

```bash
$ conda activate ht_mat
```

`ht_mat` is the name of the conda environment. Feel free to choose your own.

Install some basic packages:

```bash
$ conda install -c conda-forge pip pymatgen boto3
```

See [Conda Environment](label:conda) for more info on using conda.

## Installing workflow packages

```bash
$ pip install atomate2
```

## Configuring database outputs

Create a directory, e.g. in your home directory, to store all the config files.

```bash
$ cd ~ && mkdir ht_config_files
$ cd ht_config_files
```

Let's call this the `<CONFIG_DIR>`. In below, each time we use `<CONFIG_DIR>`, you should provide the full path, not the relative path. To get the full path, do `$ pwd`, and you should see something like:

```bash
/home/<your_username>/ht_config_files
```

### jobflow.yaml

This file specifics the MongoDB and MinIO info to store your calculation outputs. Create a `jobflow.yaml` in the `<CONFIG_DIR>` directory with the below content:

::::{tab-set}

:::{tab-item} On Carya

```yaml
JOB_STORE:
  docs_store:
    type: MongoURIStore
    uri: <uri>
    database: <database>
    collection_name: jobflow_outputs
  additional_stores:
    data:
      type: S3Store
      endpoint_url: http://10.2.1.14:9000
      bucket: <minio_bucket_name>
      key: blob_uuid
      compress: true
      index:
        type: MongoURIStore
        uri: <uri>
        database: <database>
        collection_name: jobflow_minio_index
        key: blob_uuid
      s3_profile:
        aws_access_key_id: <minio_username>
        aws_secret_access_key: <minio_password>
```

```{tip}
Replace all info in bracket `<>` by your MongoDB and MinIO access credentials. For `<uri>`, don't forget to replace `<mongo_username>` and `<mongo_password>` as well. Also, ensure the indentation is correct.
```

:::

:::{tab-item} On Sabine

```yaml
JOB_STORE:
  docs_store:
    type: MongoURIStore
    uri: <uri>
    database: <database>
    collection_name: jobflow_outputs
  additional_stores:
    data:
      type: S3Store
      bucket: <minio_bucket_name>
      key: blob_uuid
      compress: true
      index:
        type: MongoURIStore
        uri: <uri>
        database: <database>
        collection_name: jobflow_minio_index
        key: blob_uuid
      s3_profile:
        aws_access_key_id: <minio_username>
        aws_secret_access_key: <minio_password>
      ssh_tunnel:
        type: SSHTunnel
        tunnel_server_address: carya.rcdc.uh.edu:22
        remote_server_address: carya-nfs12:9000
        local_port: 9000
        username: <CARYA_USERNAME>
        password: <CARYA_PASSWORD>
```

```{tip}
Replace all info in bracket `<>` by your MongoDB and MinIO access credentials. For `<uri>`, don't forget to replace `<mongo_username>` and `<mongo_password>` as well. Also, ensure the indentation is correct.

Also, replace `<CARYA_USERNAME>` and `<CARYA_PASSWORD>` by your Carya (yes, not Sabine) username and login password (i.g. your Cougarnet password). This is needed to establish a SSH tunnel to Carya from Sabine to access the MinIO server.
```

:::
::::

### atomate2.yaml

This file specifics atomate2 settings, the commands to run VASP, update of VASP INCAR parameters, and the maximum allowed number of custodian errors, etc. You can see the full list of available settings in the [Atomate2Settings](https://materialsproject.github.io/atomate2/reference/atomate2.settings.Atomate2Settings.html#atomate2.settings.Atomate2Settings) docs.
For now we just config the commands used to run VASP.

Create an `atomate2.yaml` file in the `<CONFIG_DIR>` directory with the below content:

```yaml
VASP_CMD: mpirun --bind-to core vasp_std
VASP_GAMMA_CMD: mpirun --bind-to core vasp_gam
```

### Setting environment variables

The last thing is to set environment variables to point to these files so that joflow and atomate2 can find them.

Edit your `~/.bashrc` file and add the below two lines:

```bash
export JOBFLOW_CONFIG_FILE=<CONFIG_DIR>/jobflow.yaml
export ATOMATE2_CONFIG_FILE=<CONFIG_DIR>/atomate2.yaml
```

Remember you need to replace `<CONFIG_DIR>` by the full path to your config file directory.

```{note}
After editing `~/.bashrc`, you need to `$ source ~/.bashrc` for the change to take effect.
```

## Configuring pymatgen

To run VASP workflows, create a `~/.pmgrc.yaml` file with the below content:

```yaml
PMG_VASP_PSP_DIR: /project/wen/commons/vasp/pp
```

This will allow the use of pymatgen to automatically create pseudopotentials for your VASP calculations.

## Running a workflow

Up to this point, you've fully configured the workflow packages. Plase
try the example workflows from the [atomate2](https://materialsproject.github.io/atomate2/user/running-workflows.html) official tutorials before moving to the next session.

## Next step

Continue with [submitting jobs with fireworks](label:fireworks).

## More information

atomate2 documentation: https://materialsproject.github.io/atomate2/
