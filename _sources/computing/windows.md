(label:windows)=

# Setting up Windows

This page describes the basic steps to set up your Windows computer for computational research.
The major task is to install Windows Subsystem for Linux (WSL) and Python.

## WSL 2

WSL is Windows subsystem for Linux. More particularly we will be focusing on installing WSL 2.
What we are doing is unlocking the ability to use the Ubuntu operating system (or other Linux OS) on our Windows computer to better interact with the clusters on campus & for ease of installing & for the ability to use other utilities and packages.

First we must install WSL 2, to do this first you will have to:

::::{tab-set}

:::{tab-item} Command Line

1.  Update Windows prior to installing WSL (older version of Windows 11 did not work with this command)
2.  Type CMD into the search bar (with administrator privileges on your computer) to pull up the windows command line.
3.  On the windows command line type,

```bash
wsl --install
```

This will install WSL 2 (or the most recent iteration of WSL) onto your computer. This may ask you to restart your computer.

Windows says that this will install Ubuntu onto your computer, but this is not always the case, this is fine just install [Ubuntu]([Ubuntu - Microsoft Apps](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=en-us&gl=US)) from the windows application store. This method may not work for Windows 10

:::

:::{tab-item} Windows Feature

1. Update Windows prior to installing WSL.
2. Open the Start Menu & search `Windows Features` into the search bar. Then click on `Turn Windows Features On or Off`
3. Scroll down to the check box for `Windows Subsystem for Linux` check the box, and press the `OK` button.
4. When the operation has completed, you will be asked to restart your computer
5. After the restart install [Ubuntu]([Ubuntu - Microsoft Apps](https://apps.microsoft.com/detail/9pdxgncfsczv?hl=en-us&gl=US))from the windows application store.

:::
::::

When you finish the installation of Ubuntu and open it, you will be asked to provide a username and password. Remember the password as any time you use the sudo command you will have to enter this password. (any root level commands will prompt you for your password.). After your Ubuntu has been installed it would be a good time to use the command `sudo apt update` to update your Ubuntu installation to the most recent iteration of Ubuntu.

## Python and Python Utilities

We use Python a lot for our research and let's install Python and a series of utilities to manage our environments and packages more easily.

```bash
sudo apt install python3 –y
sudo apt install python3-pip –y
sudo apt-get install wget
wget https://repo.anaconda.com/archive/Anaconda3-2024.02-1-Linux-x86_64.sh
bash Anaconda3-2024.02-1-Linux-x86_64.sh
```

This series of commands will install: `python3`, `pip` a package downloading tool, `wget` a file downloading tool, and `conda` a Python environment managing tool.

For instructions on how to use `conda` to manage your Python environments, see [Conda Environments](label:conda).

## Jupyter Lab

We also use Jupyter Lab a lot for our research. It is a great tool for interactive computing and data visualization. To install and use Jupyter lab we will:

1.  Open the Ubuntu application from the windows start menu.
2.  Update Ubuntu
    ```bash
    sudo apt update
    ```
3.  Install Jupyter lab

    ```bash
    pip install jupyterlab
    ```

4.  Start Jupyter lab

    ```bash
    jupyter lab
    ```

5.  Once Jupyter lab has executed you will have to copy the https address in the jupyter lab output into the address bar in your favorite web browser.
6.  From here you can see your directories and files, run commands from the terminal, edit code and other things.

## Using Pycharm with WSL

Install [Pycharm](https://www.jetbrains.com/pycharm/download/?section=windows) in the normal way you would download any other program for your windows computer. After this our Pycharm will be installed onto the Windows side of our computer. Because of this the default interpreter dose not work with all the packages you have installed on your Linux version of your computer. Because of this we will have to change/update our interpreter in Pycharm to `look` for the correct interpretation of python & python packages.

1. Inside the Pycharm application, in the bottom right corner will be a tab that when you hover over it will say `Current Interpreter: ...` Click this tab
2. In the interface that opens up click the "Add New Interpreter" button, then press the `On WSL...` button
3. A window will pop up, after a moment you should see `Introspection completed successfully!` select the `Next` button in the bottom right
4. From here you could select any of the options.
   - The Virtual Environment option comes with a few issues and is not recommended to use.
   - The System Interpreter option selects your baseline python installation on the Linux side of your computer. While this can work for your programming needs it is not best practice to use this.
   - The Conda Environment option is best practice and relates to a particular Anaconda environment.
5. For Conda Environment option select "Use Existing" and select the environment you want to use for this project, or create new environment and fill in a name for the new environment
6. Press the "Create" option.
7. In the bottom corner again select the "Current Interpreter: ..." tab and select the interpreter that was just made.

## Tips/Notes

- To transfer files between Windows and WSL, see this [Stack Overflow post](https://stackoverflow.com/questions/42586120/copy-files-from-windows-to-windows-subsystem-for-linux-wsl).
- For a general Linux command cheat sheet refer to [Geeks for Geeks cheat sheet](https://www.geeksforgeeks.org/linux-commands-cheat-sheet/) here you can find a simple list of commands for Linux along with more advanced commands.
