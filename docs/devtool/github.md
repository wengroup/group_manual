# GitHub

## Cloning a repo
Generate SSH key and add it to your GitHub account, follow the tutorial here [Google link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

Click on `Code` to copy the URL
```
{figure} ../image/Git clone.png
```
Open your terminal and navigate to your working directory

Use this command to clone
```
$ git clone <URL>
``` 
Press   **Enter** to create your local clone

## Commiting changes
Navigate to your working directory  

Commit a message
```
$ git commit -m 'message'
```
Check the status
```
$ git status
```

```
$ git log
```

## Git Push
Open your terminal and move to the specific path in your local computer
```
$ cd 'path_name'
```
Initialize the repository
```
$ git init
``` 
Add the files to the new repository 
```
$ git add .
```
View all the files which are going to be staged to the first commit
```
$ git status
```
Use the command to commit a message 
```
$ git commit -m 'your message'
``` 
```
$ git branch -M main
```
Add the URL copied, which is your remote repository to where your local content from your repository is pushed 
```
$ git remote add origin <URL>
```
Push the code in your local repository to Github 
```
$ git push -u origin main
```



