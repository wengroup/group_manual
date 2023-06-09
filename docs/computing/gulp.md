# GULP
1. Navigate to the GULP download page by visiting this [link](https://gulp.curtin.edu.au/download.html).
2. Input your Cougarnet email address in the following format: `[username@cougarnet.uh.edu]` to request GULP.
3. After submitting your email, you should receive an email containing a .tgz file. Download this file to your local device.
4. Now, log into your Carya account. There, create a new directory named "gulp" on the `/project/wen/<your_username>` path. (If you have not created this before check conda environment page, changing environment directory) You can achieve this by using the command: `mkdir gulp`.
5. Next, transfer the .tgz file you downloaded from your local device to the newly created 'gulp' directory on Carya using `scp </local/path/gulp.tgz> <your_username>@carya.rcdc.uh.edu:</project/wen/<your_username>`.
6. Once you have the .tgz file in the correct location, use `module load python` to load python and miniconda. Then create a new environment named 'gulp' by executing: `conda create -n gulp`.
7. After creating the environment, activate it by entering: `conda activate gulp`.
8. Now, install the Scalapack package to your active Conda environment by typing: `conda install -c conda-forge scalapack`.
9. With Scalapack installed, extract the contents of the .tgz file by using the command: `tar -xvf <tgz file name>`.
10. Navigate to the 'Src' directory in the extracted 'gulp-6.1.2' folder by typing: `cd gulp-6.1.2/Src`.
11. In this directory, compile the required files using gfortran with the command: `./mkgulp_old_gfortran`.
12. To run GULP you will have to execute the gulp file in Src directory by doing `/project/wen/<your_username>/<gulp_version>/Src/gulp`.

If for some reason, GULP doesn't run after following these steps, do the following:

1. Verify that the GULP executable is within your path. Do this by typing `which gulp`.
2. If the executable is in your current directory, type `./gulp` to confirm its visibility.

By following these instructions, you should be able to download, install, and use GULP successfully.
