# Set up mutiple accounts for github in local
Ref: https://blog.gitguardian.com/8-easy-steps-to-set-up-multiple-git-accounts/

Using SSH to set up github account. one SSH keypair = one Git config and structure the workspace accourding to different accounts.

## Generate an SSH key
It is upto user to use ed25519 or rsa. ed25519 is remmended though
ssh-keygen -t ed25519 -C "email@example.com" -f ~/.ssh/<personal_key_file_name> 

When you generate your key, tt is not mandantory, but recommened for security purpose. 
Incase you want to update your paraphase, use this sweet command
ssh-keygen -p -f ~/.ssh/<personal_key_file_name> 

## Update ssh-agent
eval "$(ssh-agent -s)" && \
ssh-add --apple-use-keychain ~/.ssh/<personal_key> 

apple-use-keychain is for mac only

## Update ssh config file

Update file ~/.ssh/config with github
```
Host github.com
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes  
  IdentityFile ~/.ssh/<key_file_name>

# Personal GitHub account
Host github-personal
  HostName github.com
  User git
  AddKeysToAgent yes
  UseKeychain yes    
  IdentityFile ~/.ssh/<personal_key_file_name>
```

## Update your SSH public key in your github
- Open the public key <personal_key_file_name>.pub update the public key in your github

## Structure your workspace
We need a way to tell git which creds it needs to use. So we have to struct the workspace. For example
/home ~/
    |__.gitconfig
    |__work/
    |__personal/

## Update config files for git
- Create 2 config files (or more if needed): work.config and personal.config
```
    # config file for work/

    [user]
        email = sth  
        name = sth
    [core]
        sshCommand = "ssh -i ~/.ssh/work_keyfile"
```

```
    # config file for personal/
    [user]
        email = sth     
        name = sth
    [url "git@github-personal"]
        insteadOf = git@github.com
    [core]
        sshCommand = "ssh -i ~/.ssh/<personal_key_file_name>"
```
Note: Make sure using the right quote "" for the files or you will be deep in pain

And now we add these to the `master` config file
```
    # ~/.gitconfig
    [core]
        excludesfile = ~/.gitignore_global
    [includeIf "gitdir/i:~/path/to/personal/workspace"] 
        path = ~/path/to/this/personal.gitconfig
    [includeIf "gitdir/i:~/path/to/work/space"]
        path = ~/path/to/this/work.gitconfig
    ```

The work i is for not case sensitive

If you do have nother account for gitlab, aws codecommit, bitbucket, etc, only need to update the ~/.ssh/config file with right host, user and identify file