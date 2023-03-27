(label:ssh)=
# SSH

## Generating an SSH keys 

- Open your terminal and enter the following command. Change the `your_email@gmail.com`
  to your own email address or other comments.
```
$ ssh-keygen -t rsa -b 4096 -C "your_email@gmail.com"
```
- This will start the process of generating your SSH key and you will be directed to enter a file name for the key.   
- Press **Enter** to accept the default file names (`id_rsa` for the private key and 
  `id_rsa.pub` for the public key) and the default location (`~/.ssh` directory).  
- Enter a passphrase for the key. This is optional but highly recommended for added 
  security.(Pressing **Enter** to leave it blank will not use any passphrase.)

Don't share with others your private key at `~/.ssh/id_rsa` and passphrase.

You can view the public key by:
```
$ cat ~/.ssh/id_rsa.pub
```

## Adding the ssh key to the ssh-agent
We refer to [Github instructions on generating SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)
## More information

- [Github instructions on generating SSH keys](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
