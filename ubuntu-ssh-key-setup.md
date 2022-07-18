## Steps to set-up SSH keys for GitHub in Ubuntu
> This method is useful when you want to setup SSH keys for multiple accounts

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

4. Create a github configuration file at account level (`~/clients/git/<github_uname>/gitconfig.<github_uname>`)
    * Here, inside the `git` folder, you'll have your multiple GitHub accounts and their config files inside it
    ```
    [user]
    email = <github_email>
    name = <github_name>
    
    [github]
    user = <github_username>
    ```

5. Next step is to add the ssh keys that we created
    ```
    ssh-add ~/.ssh/github/<private_ssh_key> 
    ssh-keyscan >> ~.ssh/known_hosts
    ```

6. Now, we add the public ssh key (`~/.ssh/github/<ssh_key>.pub`) in our GitHub account from the web browser

7. Next step is to sit back and relax because the SSH keys have been successfully added. To verify, you can run the following command
    ```
    $ ssh -T git@github.com-<github_username>
    $ Hi GitHub user! You've successfully authenticated, but GitHub does not provide shell access.
    ```
    * You mention the host with `-T` flag. This is the host that we mentioned in the `~/.ssh/config` file

## Multi-account SSH Key setup
You follow the same steps to add another GitHub account. But, you don't need to modify anything inside the global configuration file because the local configuration file inside `~/git/clients/<github_uname>/` will override the global config file, thus providing the right credentials.
___
> Note:   
>When you perform git operations (pull/clone) with the repo, make sure you mention the correct hostname. For example, 
```
SSH Link from GitHub repository (Browser) -> git@github.com:masif2002/fastapi.git
Incorrect 'clone' command -> git clone git@github.com:masif2002/fastapi.git
Correct 'clone' command -> git clone git@github.com-masif2002:masif2002/fastapi.git
```
