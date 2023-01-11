# Arch Linux - Packages
## Git
- Install
  ```
  sudo pacman -S git
  ```
- Setup
  - Configure Git  
    Replace the `name` and `email` with your name and email
    ```
    git config --global user.name "Magic Unicorn"
    git config --global user.email magic@unicorn.com
    ```
  - Create the `.shh` directory
    ```
    sudo mkdir -p ~/.ssh
    ```
  - Verify that you have the permissions on the `.ssh` directory  
    Use `ls -a -l` to see the permissions
    ```
    sudo chown -R $USER:$USER ~/.ssh
    ```
  - Generating a new SSH key
    ```
    ssh-keygen -t ed25519 -C "magic@unicorn.com" 
    ```
  - Change the permissions on the SSH key  
    Replace `{ssh_key}` by your SSH key name
    ```
    chmod 400 ~/.ssh/{ssh_key}
    ```
  - Create a `config` file 
    ```
    nano ~/.ssh/config
    ```
  - Add this to the `config` file  
    Replace `{magicunicorn}` by your github username and `{ssh_key}` by your SSH key name
    ```
    Host github.com
    User {magicunicorn}
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/{ssh_key}
    IdentitiesOnly yes
    ```
  - Change the permissions on the `config` file
    ```
    chmod 600 ~/.ssh/config
    ```
  - Read and copy the `public key`  
    Replace `{ssh_key}` by your SSH key name
    ```
    cat ~/.ssh/{ssh_key}.pub
    ```
  - Add the `public key` to your `Github account`
    ```
    https://github.com/settings/keys
    ```
  - Etablish a SSH connection
    ```
    ssh -T git@github.com
    ```
