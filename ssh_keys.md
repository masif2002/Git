## SSH Keys

### 1. Generating SSH key
___
* To establish a connection between a remote repository and our local machine, we need to generate SSH keys.
 
* Command for generating ssh key:

  ```
  ssh-keygen -t rsa -b 4096 -C "masif2002@gmail.com"
  ```

    -t &rarr; type of encryption  
    -b &rarr; strength of encryption  
    -C &rarr; email address  

Two files will be generated:
+ [file] key - private key, which will be used to verify you are the owner of the account with so and so public key.

+ [file] key.pub - public key, which you need to update in your code-hosting site (like GitHub) under the SSH section

### 2. Adding the SSH key to the ssh-agent
___

+ You can start the ssh-agent manually by running     
`eval "$(ssh-agent -s)"`

```
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

+ Add your SSH private key to the ssh-agent
```
$ ssh-add ~/.ssh/id_rsa
```
You need to replace *id_rsa* with the name of your private key file
