# GitHub
GitHub is a web-based platform that provides tools for version control and collaborative software development. It allows developers to host their code repositories online, track changes to code over time, and work together with others on the same codebase.  
## Generating an SSH key
* Open your terminal and enter the following command. Use the rsa algorithm to generate the key because of wider support. Where you can change the your_email address to yours.
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@gmail.com"
```
* This will start the process of generating your SSH key and you will be directed to enter a file name for the key.   
* Press **Enter** to accept the default file name and location.  
* Enter a passphrase for the key. This is optional but highly recommended for added security.   
* Press **Enter** to leave it blank. Once the key is generated, you can view the public key by entering the following command in your terminal:
```
$ cat ~/.ssh/id_rsa.pub
```
* Highlight and copy the entire public key to your clipboard.
```{figure} ../image/COPY SSH.png

``` 
## Uploading to GitHub
* Log in to your GitHub account and click on your profile picture in the top-right corner of the page. 
```{figure} ../image/Profile.png

```
* Select **Settings** from the dropdown menu and in the left sidebar, click on "SSH and GPG keys".  
* Click on the green **New SSH key** button and give your SSH key a descriptive title in the **Title** field.
```{figure} ../image/Title.png

```
* Paste the entire public key you copied earlier into the **Key** field and click on the green **Add SSH key** button.  
* Your SSH key is now uploaded to GitHub and you can now use SSH to authenticate with GitHub and perform various Git operations.

## Cloning a repository
* Open your terminal on your laptop.  
* Clone the repository using the SSH URL. For example, if the repository URL is `git@github.com:USERNAME/REPOSITORY.git`. USERNAME and REPOSITORY need to be change to your own. You can clone it by running this command:
```
$ git clone git@github.com:USERNAME/REPOSITORY.git
```
```{figure} ../image/SSH.png

```
* Navigate to the cloned repository using the **cd** command.
```
$ cd REPOSITORY
```
## Making changes
* Make the changes you want using your desired text editor.  
* Stage all the changes you made using the **git add** command.
```
$ git add .
```
## Committing changes
* Commit the changes using the **git commit** command. Where the commit message is the changes you made.
```
$ git commit -m 'commit message'
```
## Push the changes
* Push the changes using **git push** command.
```
$ git push 
```
## Pull request
* Go to the repository on github and click on **pull request** tab
and then click on the green **New pull request button**.   
```{figure} ../image/Pull.png

```
* Select the branch with your changes from the **base** dropdown menu and the branch you want to merge into from the **compare** dropdown menu.
* Review the changes in the pull request and add a descriptive title and description. Click on the green **Create pull request** button. 
* Write a description of changes made and click on **Create pull request button**. The pull request will be sent to the repository owner for necessary review.

## More information  
* Github skills  
https://skills.github.com/  
* Generating SSH keys:  
https://www.flownative.com/en/documentation/guides/beach/how-to-generate-a-new-ssh-key-and-add-it-to-the-ssh-agent.html
