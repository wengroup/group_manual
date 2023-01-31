# VASP

## VASP on Carya

### Getting access to VASP

To check the available VASP modules, do

```
$ module avail vasp
```

Then select one from the list and load it, e.g.

```
$ module load vasp-wen/6.3.2
```

### Run a first VASP jobs

The example performs a relaxation of a Si diamond structure. First, create a directory and put into it the below three files. The names of the files should `INCAR`, `POSCAR` and `POTCAR`.

::::{tab-set}

:::{tab-item} INCAR

INCAR is the central input file of VASP.

```
IBRION = 2
NSW = 99
NELM = 200
PREC = Accurate
ALGO = Normal
ENCUT = 500
EDIFF = 1e-5
ISIF = 3
ISMEAR = -5
SIGMA = 0.2
ISPIN = 2
KSPACING = 0.22
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

:::{tab-item} POTCAR
POTCAR gives the poeudopotential.

POTCAR is proprietary, and we cannot list it publicly. To get it, on `Carya`, copy `/project/wen/commons/vasp/pp/potpaw_PBE_54/Si/POTCAR` to your directory.

:::
::::

Then, in the directory, submit the job using the below Slurm script.

````
```bash
#!/bin/bash -l

#SBATCH --job-name=vasp_job
#SBATCH --account=wen
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=24
#SBATCH --mem=50GB  # max 189 GB

module load vasp-wen/6.3.2

mpirun -n 24 --bind-to core vasp_std
````

```{note}
In some other tutorials, you may find that in addition to the above three, another `KPOINT` filed is provided to specify the meshes in the reciprocal space. Here, we use an alternative approach by providing the `KSPACING` value in the `INCAR` file.
```

### VASP data files

Pseudopotentials are located at: `/project/wen/commons/vasp/pp`

Vdw kernels are located at: `/project/wen/commons/vasp/vdw_kernel`
