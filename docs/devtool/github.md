# GitHub



## Procedures to cloning a repository, making changes, commit, push and create a pull request
Open your terminal on your laptop  
Navigate to the directory you want to clone using **cd** command
```
$ cd /path/to/directory
```
Use the **git clone** command to clone the repository. This will create a copy of the repository on your local machine.
```
$ git clone https://github.com/<username>/<repository-name>.git
```
Navigate to the cloned repository using the **cd** command
```
$ cd <repository-name>
```
Create a new branch for your changes using the **git checkout** command
```
$ git checkout -b <branch-name>
```
Make the changes you want using your desired text editor  
Stage all the changes you made using the **git add** command
```
$ git add .
```
Commit the changes using the **git commit** command. Where the commit message is the changes you made
```
$ git commit -m 'commit message'
```
Push the changes using **git push** command
```
$ git push origin <branch-name>
```
Go to the repository on git hub and click on **Compare & pull request** button  
Write a description of changes made and click on **Create pull request button**  
The pull request will be sent to the repository owner for necessary review
**More information**  
Github skills: https://skills.github.com/
