(label:git)=

# Git
Git allows developers to keep track of changes to their code, collaborate with other developers, and work on multiple versions of their software simultaneously. This is achieved through a distributed model, where each developer has a copy of the codebase on their local machine and can make changes and commit them to a shared repository.

## Install Git
You can download Git from the official website: https://git-scm.com/downloads

If you use Mac, first install [Homebrew](https://brew.sh/index_zh-tw.html), you can use Homebrew to install Git, and execute this line of command in the terminal to complete:
```
$ brew install git
```

## Set up the Git environment
Once Git is installed, you'll need to set up your environment by configuring your username and email address, so that Git can attribute your changes to you. To do this, open a command prompt or terminal window and type the following commands, replacing "Your Name" and "Youremail" with your own information:
```
$ git config --global user.name "Your Name"
$ git config --global user.email "Youremail@example.com"
```

## Git workflow and basic commands
<img width="820" alt="image" src="https://user-images.githubusercontent.com/123142931/219302278-e9655f60-d6b6-4594-a0fc-4a649c6e11d0.png">


### Create a new repository to start using Git.
```
$ git init
```

### Add files from workspace (working directory) to staging area (first level).
```
$ git add <filename>
```

### You can also use 'git add .' to add all files in the current directory to the staging area.
```
$ git add .
```

### Transfer files from staging (first level) to repository (second level).
```
$ git commit
```

### Add message to full history to record your own changes.
```
$ git commit -m "Commit message"
# Replace "Commit message" with a brief description of the changes you're committing.
```

### Show full history of Git repository. This will show you a list of all the commits that have been made to the repository, including the commit message, the author, and the date and time.
```
$ git log
```

### View the before and after changes of files.
```
$ git diff
```

### Check the status of your Git repository at any time. This will show you which files have been modified or added, which files are currently in the staging area, and which files have been committed to the repository.
```
$ git status
```

### Restore the last action on files.
```
$ git restore <filename>
```

### View current remote connection location (SSH).
```
$ git remote -v
```

### Transfer files from local repository to a remote repository (Github).
```
$ git push <filename>

```
### Transfer files from remote repository (Github) to the workspace.
```
$ git pull <filename>
```

### Retrieve changes from a remote repository without merging them into your local repository(branch). This means that you can review the changes and decide whether to merge them into your branch or not. This gives you more control over the merging process and can help you avoid conflicts when multiple contributors are working on the same codebase.
```
$ git fetch <filename>
```

### Integrate changes from one branch into another.
```
$ git merge <filename>
```

## Git tutorial
https://swcarpentry.github.io/git-novice/
