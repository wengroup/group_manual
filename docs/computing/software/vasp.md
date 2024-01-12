# VASP

```{warning}
The below instructions apply to the HPE DSI `Carya` and `Sabine` clusters.
```

## Getting access to VASP

To check the available VASP modules, do

```
$ module avail vasp
```

Then select one from the list and load it, e.g.

```
$ module load vasp-wen/6.4.2
```

## Run a first VASP jobs

The example performs a relaxation of a Si diamond structure. First, create a directory and put into it the below three files. The names of the files should `INCAR`, `POSCAR` `KPOINTS`, and `POTCAR`.

::::{tab-set}

:::{tab-item} INCAR

INCAR is the central input file of VASP.

```
IBRION = 2
NSW = 99
NELM = 200
PREC = Accurate
ALGO = Normal
ENCUT = 520
EDIFF = 1e-5
ISIF = 3
ISMEAR = -5
SIGMA = 0.2
```

:::

:::{tab-item} POSCAR

POSCAR gives the atomic structure of the material.

```
Diamond silicon structure
1.0
3.348898 0.000000 1.933487
1.116299 3.157372 1.933487
0.000000 0.000000 3.866975
Si
2
direct
0.250000 0.250000 0.250000 Si
0.000000 0.000000 0.000000 Si
```

:::

:::{tab-item} KPOINTS

KPOINTS gives the Bloch vectors to sample the Brillouin zone.

```

k grid mesh
0
Gamma
4 4 4

```

:::

:::{tab-item} POTCAR
POTCAR gives the pseudopotential.

POTCAR is proprietary, and we cannot list it publicly. To get it, on `Carya` or `Sabine`, copy `/project/wen/commons/vasp/pp/POT_GGA_PAW_PBE_54/Si/POTCAR` to your directory.

:::
::::

Then, in the directory, submit the job using the below Slurm script.

::::{tab-set}

:::{tab-item} Sabine

```bash
#!/bin/bash -l

#SBATCH --job-name=vasp_job
#SBATCH --account=wen
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=24
#SBATCH --mem=50GB  # max 189 GB

#SBATCH --exclusive

module load vasp-wen/6.4.2

mpirun -n 24 --bind-to core vasp_std
```

```{warning}
Don't forget to add the `#SBATCH --exclusive` line, otherwise your MPI job will fail if other users are trying to run MPI jobs on the same node.
This is not needed on `Carya`.
```

:::

:::{tab-item} Carya

```bash
#!/bin/bash -l

#SBATCH --job-name=vasp_job
#SBATCH --account=wen
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=24
#SBATCH --mem=50GB  # max 189 GB

module load vasp-wen/6.4.2

mpirun -n 24 --bind-to core vasp_std
```

:::
::::

```{note}
In some other tutorials, instead of using the `KPOINTS` file, you can add a  `KSPACING` value in the `INCAR` file to automatically generate the k-points mesh.
```

## VASP data files

Pseudopotentials are located at: `/project/wen/commons/vasp/pp`

Vdw kernels are located at: `/project/wen/commons/vasp/vdw_kernel`
