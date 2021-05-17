# Ansible-ConUp
Case Senario: Need Ansible for a number of managed nodes/servers, without their passwords shared, via a public/private key.

## To be run on all target nodes, CentOS, RHEL, Other Linux

### 1. Create a new user :
> $ sudo adduser ansible_user\
> $ sudo passwd ansible_user\
> Changing password for user ansible_user.\
> New password: \
> Retype new password: \
> passwd: all authentication tokens updated successfully.\

### 2. Add it to the sudoers group
> $ sudo usermod -aG wheel ansible_user

### 3. Edit sudoers
> $ sudo vi /etc/sudoers

### 4. At the bottom of the file, please add the following line.
> ansible_user ALL=(ALL) NOPASSWD:ALL

### 5. Save and Exit



## To be run on ansible engine, Ubuntu OS

### 1. Create a new user :
> $ sudo adduser ansible_user\
> [sudo] password for dinu: \
> Adding user `ansible_user' ...\
> Adding new group `ansible_user' (1001) ...\
> Adding new user `ansible_user' (1001) with group `ansible_user' ...\
> Creating home directory `/home/ansible_user' ...\
> Copying files from `/etc/skel' ...\
> New password: \
> Retype new password: \
> passwd: password updated successfully\
> Changing the user information for ansible_user\
> Enter the new value, or press ENTER for the default\
> 	Full Name []: \
>   Room Number []: \
> 	Work Phone []: \
>   Home Phone []: \
>   Other []: \
> Is the information correct? [Y/n] Y

### 2. Add it to the sudoers group
> $ sudo usermod -aG sudo ansible_user

### 3. Become the user
> $ su ansible_user$ su ansible_user\
> Password: \
> To run a command as administrator (user "root"), use "sudo <command>".\
> See "man sudo_root" for details.

### 4. Create a Key
> $ ssh-keygen\
> Generating public/private rsa key pair.\
> Enter file in which to save the key (/home/ansible_user/.ssh/id_rsa): \
> Created directory '/home/ansible_user/.ssh'.\
> Enter passphrase (empty for no passphrase): \
> Enter same passphrase again: \
> Your identification has been saved in /home/ansible_user/.ssh/id_rsa\
> Your public key has been saved in /home/ansible_user/.ssh/id_rsa.pub\
> The key fingerprint is:\
> SHA256:NMtyZKb6e0Hr2bktLEkNAgm/2EFpxlXO9qsWZ/P0zjU ansible_user@dinu\
> The key's randomart image is:\
> +---[RSA 3072]----+\
> |  .o.+...        |\
> |   oB  o         |\
> |   oo.  X        |\
> |   o o.Oo+       |\
> |  . o ooS+.      |\
> |     . o= =..    |\
> |    .  o X.= . E.|\
> |     .  B.=......|\
> |      o+...o..o  |\
> +----[SHA256]-----+\
> $ ls -a\
> .   .bash_history  .bashrc   .ssh\
> ..  .bash_logout   .profile  .sudo_as_admin_successful

### 5. Now that the key is created, run it on all the managed nodes

### Syntax :
### ssh-copy-id -i ~/.ssh/id_rsa.pub    ansible_user@ip_address

> $ ssh-copy-id -i /home/ansible_user/.ssh/id_rsa.pub    ansible_user@192.168.1.x\
> /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ansible_user/.ssh/id_rsa.pub"\
> The authenticity of host '192.168.1.x (192.168.1.x)' can't be established.\
> ECDSA key fingerprint is SHA256:nmvCr9t1FV2YPTIxF8mZOjfYMimUCgs6sBszpgnjtlk.\
> Are you sure you want to continue connecting (yes/no/[fingerprint])? yes\
> /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed\
> /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys\
> ansible_user@192.168.1.6's password: 

### 6. Number of key(s) added: 1

### 7. Now try logging into the machine, with:   "ssh 'ansible_user@192.168.1.x'"
### 8. And check to make sure that only the key(s) you wanted were added.

### 9. Verify if SSH is working :

### Syntax:
### ssh ansible_user@ip_address

> $ ssh ansible_user@192.168.1.x\
> Activate the web console with: systemctl enable --now cockpit.socket
