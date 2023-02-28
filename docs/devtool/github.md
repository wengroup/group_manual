# GitHub

## Generating an SSH key and upload to GitHub
Open your terminal and eneter the following command:
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
Use the rsa algorithm to generate the key because of wider support  
This will start the process of generating your SSH key  
You will be directed to enter a file name for the key   
Press **Enter** to accept the default file name and location  
You will then be prompted to enter a passphrase for the key.       This is optional but highly recommended for added security   
Press **Enter** to leave it blank  
Once the key is generated, you can view the public key by entering the following command in your terminal:
```
$ cat ~/.ssh/id_rsa.pub
```
Highlight and copy the entire public key to your clipboard  
Log in to your GitHub account and click on your profile picture in the top-right corner of the page 
```{figure} ../image/Screenshot 2023-02-28 at 11.10.10 AM.png

```
Then select **Settings** from the dropdown menu  
In the left sidebar, click on "SSH and GPG keys"  
Click on the green **New SSH key** button  
Give your SSH key a descriptive title in the **Title** field
```{figure} ../image/Screenshot 2023-02-28 at 11.10.31 AM.png

```
Paste the entire public key you copied earlier into the **Key** field  
Click on the green **Add SSH key** button  
Your SSH key is now uploaded to GitHub and ready to use  
You can now use SSH to authenticate with GitHub and perform various Git operations.

## Procedures to cloning a repository, making changes, commit, push and create a pull request
Open your terminal on your laptop  
Clone the repository using the SSH URL. For example, if the repository URL is 'git@github.com:USERNAME/REPOSITORY.git'. You can clone it by running this command:
```
$ git clone git@github.com:USERNAME/REPOSITORY.git
```
```{figure} ../image/Screenshot 2023-02-28 at 11.02.42 AM.png

```
Navigate to the cloned repository using the **cd** command
```
$ cd REPOSITORY
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
$ git push 
```
Go to the repository on git hub and click on **pull request** tab
and then click on the green **New pull request button**   
```{figure} ../image/Screenshot 2023-02-28 at 11.07.38 AM.png

```
Select the branch with your changes from the **base** dropdown menu and the branch you want to merge into from the **compare** dropdown menu
Review the changes in the pull request and add a descriptive title and description  
Click on the green **Create pull request** button  
Write a description of changes made and click on **Create pull request button**  
The pull request will be sent to the repository owner for necessary review
**More information**  
Github skills: https://skills.github.com/
