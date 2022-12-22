# Set up mutiple accounts for github in local
Ref: https://blog.gitguardian.com/8-easy-steps-to-set-up-multiple-git-accounts/

Using SSH to set up github account. one SSH keypair = one Git config

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