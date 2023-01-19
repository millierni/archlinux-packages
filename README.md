# Arch Linux - Packages
## GIT
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
## NEOFETCH
- Install
  ```
  sudo pacman -S neofetch
  ```
## WGET
- Install
  ```
  sudo pacman -S wget
  ```
## HTOP
- Install
  ```
  sudo pacman -S htop
  ```
## SQLITEBROWSER
- Install
  ```
  sudo pacman -S sqlitebrowser
  ```
## NMAP
- Install
  ```
  sudo pacman -S nmap
  ```
## STEAM
- Install
  ```
  sudo pacman -S steam
  ```
## FIREFOX
- Install
  ```
  sudo pacman -S firefox
  ```
- Setup
  - Tweak Firefox for privacy (optional)
    ```
    https://github.com/arkenfox/user.js
    https://www.unixsheikh.com/articles/choose-your-browser-carefully.html
    https://www.youtube.com/watch?v=GVOcElOPs8E
    ```
## CUPS
- Install
  ```
  sudo pacman -S cups
  ```
- Setup
  - Start cusp deamon service
    ```
    sudo systemctl enable cups.service
    sudo systemctl start cups.service
    ```
  - Add a printer  
    Replace `{printer_name}` and `{printer_ip_address}` by your printer name and address
    ```
    sudo lpadmin -p {printer_name} -E -v ipp://{printer_ip_address}/ipp/print -m everywhere
    ```
## YAY
- Install
  ```
  git clone https://aur.archlinux.org/yay.git
  sudo chown -R $USER:$USER yay
  cd yay
  makepkg -si
  cd ..
  sudo rm -R yay
  ```
## VSCODIUM
- Install
  ```
  yay -S vscodium-bin
  ```
## KVM, QEMU, VIRT MANAGER
- Install
  ```
  sudo pacman -S qemu virt-manager virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat
  sudo pacman -S ebtables iptables
  ```
- Setup
  - Start KVM libvirt daemon service
    ```
    sudo systemctl enable libvirtd.service
    sudo systemctl start libvirtd.service
    ```
  - Verify that it's running
    ```
    systemctl status libvirtd.service
    ```
  - Edit `libvirtd.conf` and uncomment `unix_sock_group` and `unix_sock_rw_perms`
    ```
    sudo nano /etc/libvirt/libvirtd.conf
    ```
    ```
    #unix_sock_group = "libvirt"
    unix_sock_group = "libvirt"
    ```
    ```
    #unix_sock_rw_perms = "0770"
    unix_sock_rw_perms = "0770"
    ```
  - Add your user to libvirt group
    ```
    sudo usermod -a -G libvirt $(whoami)
    newgrp libvirt
    ```
  - Restart libvirt deamon
    ```
    sudo systemctl restart libvirtd.service
    ```
  - Enable Nested Virtualization feature  
    - AMD CPU
      ```
      sudo modprobe -r kvm_amd
      sudo modprobe kvm_amd nested=1
      echo "options kvm-amd nested=1" | sudo tee /etc/modprobe.d/kvm-amd.conf
      systool -m kvm_amd -v | grep nested   # verify that Nested Virtualization is enable
      cat /sys/module/kvm_amd/parameters/nested   # verify that Nested Virtualization is enable
      ```
    - Intel CPU
      ```
      sudo modprobe -r kvm_intel
      sudo modprobe kvm_intel nested=1
      echo "options kvm-intel nested=1" | sudo tee /etc/modprobe.d/kvm-intel.conf
      systool -m kvm_intel -v | grep nested   # verify that Nested Virtualization is enable
      cat /sys/module/kvm_intel/parameters/nested   # verify that Nested Virtualization is enable
      ```
- Optional
  - [Create Virtual Machine](https://github.com/millierni/vm-new-virtual-machine)
  - [CPU Pinning](https://github.com/millierni/vm-cpu-pinning)
  - [GPU Passthrough](https://github.com/millierni/vm-gpu-passthrough)
  - [Keyboard & Mouse Passthrough](https://github.com/millierni/vm-keyboard-mouse-passthrough)
## UNREAL ENGINE 5
- Install  
  https://docs.unrealengine.com/5.0/en-US/building-unreal-engine-from-source/
  ```
  git clone git@github.com:EpicGames/UnrealEngine.git
  ```
## PIPER
- Install
  ```
  sudo pacman -S piper
  ```
## LIBREWOLF
- Install
  ```
  git clone https://aur.archlinux.org/librewolf.git
  cd librewolf
  makepkg -si
  ```
