# GULP

This memo discusses the steps to download, install, and use GULP on `Carya`.

1. Navigate to the GULP download page by visiting this [link](https://gulp.curtin.edu.au/download.html).
2. Input your Cougarnet email address in the following format to request GULP:

```
<username>@cougarnet.uh.edu
```

3. After submitting your email, you should receive an email containing a .tgz file. Download this file to your local device.
4. Now, log into your Carya account. There, create a new directory named "gulp" on the

```
/project/wen/<your_username>
```

If you have not create this before check conda environment page, changing environment directory. You can achieve this by using the command:

```
$ mkdir gulp
```

5. Next, transfer the .tgz file you downloaded from your local device to the newly created 'gulp' directory on Carya using

```
scp </local/path/gulp.tgz> <your_username>@carya.rcdc.uh.edu:/project/wen/<your_username>
```

6. Once you have the .tgz file in the correct location, use this command to load python and miniconda.

```
$ module load python
```

7. Then create a new environment named 'gulp_env' by executing:

```
$ conda create -n gulp_env
```

8. After creating the environment, activate it by entering:

```
$ conda activate gulp_env
```

9. Now, install the `Scalapack` package to your active Conda environment by typing:

```
$ conda install -c conda-forge scalapack
```

10. With Scalapack installed, extract the contents of the .tgz file by using the command:

```
$ tar -xvf <tgz file name>
```

11. Navigate to the `Src` directory in the extracted `gulp-6.1.2` folder by typing:

```
$ cd gulp-6.1.2/Src
```

12. In this directory, compile the required files using gfortran with the command:

```
./mkgulp_old_gfortran
```

13. To run GULP you will have to execute the gulp file in Src directory by doing

```
/project/wen/<your_username>/gulp-6.1.2/Src/gulp
```

This requires the typing of the full path to the `gulp` executable, which is
cumbersome. To avoid this, you can edit `~/.bashrc` to append the path to the
directory of the executable to the `PATH` variable or create an alias there.
After this, you will be able to directly use `gulp` anywhere.
