## Steps to set-up SSH keys for GitHub in Ubuntu
>  [Resource: Setting up multiple git identities](https://gist.github.com/bgauduch/06a8c4ec2fec8fef6354afe94358c89e)  

## Walkthrough
1. First you need to generate an SSH key and save it save it in `~/.ssh/github/`
    ```
    ssh-keygen -t ed25519 -O "<your email>"
    ```
    * Optional parameters:
        * `-t` -> For specifying algorithm. Uses 'rsa' algo if not specified
        * `-O` -> For comment

2. Next, (create and) edit `config` file in `~/.ssh` directory
    ```
    Host github.com-<github_username>
    HostName github.com
    User git
    IdentityFile /home/asif/.ssh/github/<ssh_privatekey_file_name>

    Host *
    ServerAliveInterval 240
    ```

3. Create a global github configuration file in the root directory (`~/.gitconfig`)
    ```
    [user]
        name = <github_username>
        email = <github_email>
    [core]
        excludesfile = ~/.gitignore
    [cola]
        spellcheck = false
        icontheme = dark
        theme = flat-dark-red
        boldheaders = true
        statusshowtotals = true
        statusindent = true
    [init]
	defaultBranch = ""
    ```
    * If you want to add multiple identities instead of a single one, you can do so
        ```
         [includeIf "gitdir:~/code/personal/"]
            path = .gitconfig-personal
         [includeIf "gitdir:~/code/professional/"]
            path = .gitconfig-professional
        ```
5. Next step is to add the ssh keys that we created
    ```
    ssh-add ~/.ssh/github/<private_ssh_key> 
    ```

6. Now, we add the public ssh key (`~/.ssh/github/<ssh_key>.pub`) in our GitHub account from the web browser

7. Next step is to sit back and relax because the SSH keys have been successfully added. To verify, you can run the following command
    ```
    $ ssh -T git@github.com-<github_username>
    $ Hi GitHub user! You've successfully authenticated, but GitHub does not provide shell access.
    ```
    * You mention the host with `-T` flag. This is the host that we mentioned in the `~/.ssh/config` file

### Note   
* When you perform git operations (pull/clone) with the repo, make sure you mention the correct hostname. For example, 
    ```
    SSH Link from GitHub repository (Browser) -> git@github.com:masif2002/fastapi.git
    Incorrect 'clone' command -> git clone git@github.com:masif2002/fastapi.git
    Correct 'clone' command -> git clone git@github.com-masif2002:masif2002/fastapi.git
    ```
