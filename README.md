## ph2-vagrant Ubuntu 22.04 (Jammy)
This build uses vagrant box [ubuntu/jammy64](https://app.vagrantup.com/ubuntu/boxes/jammy64)

Prerequisite software on your host machine:
- [Vagrant](https://www.vagrantup.com/)
- [Oracle VM VirtualBox ]([https://www.vagrantup.com/](https://www.virtualbox.org/)) 

Tools included in this build:
- Terraform
- Nodejs 18
- Docker - Docker Compose

Revise line 36 in ***Vagrantfile*** accordingly to your local environment.

Revise following configuration in ***playbook.yml*** accordingly to your need:
- SSH key importing: task 13
- AWS credential configuration: task 14
- bashrc alias: task 16

Note:
***playbook.yml***
Task 13:
- Mandatory since we'll be using those credential to SSH into our box.
- Make sure to place your SSH key pair into shared folder, or task 13 will fail.
- A good practice is to have both 2 key pairs, one for RSA and another one for ED25519.
Task 14 is optional, if you do not have/do not need to set up AWS credential, simply comment it out.
Task 16 is optional, comment it out if you do not need to set up bashrc in prior.

***Vagrantfile***
Line 26 in  specify port-forwarding value for SSH connection from your host machine

Build your VM
Open CMD in your working directory and run
```
vagrant up
```
Re-run ansible playbook if needed
```
vagrant up --provision
```
After Vagrant finish provisioning your box, it'll create a VM in your Oracle VM VirtualBox.

In order to SSH into your VM box:
```
Hostname/IP: 127.0.0.1/localhost
User: vagrant
Port: 2222
```

If you are working with Visual Code Studio, install following extension to enable SSH and remote browsing:
[Remote - SSH](https://code.visualstudio.com/blogs/2019/10/03/remote-ssh-tips-and-tricks)
Remote Explorer
Remote - SSH config file
```
Host [name_your_box]
  HostName 127.0.0.1
  User vagrant
  Port 2200
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile [path_to_your_SSH_private_key_on_host_machine]
  IdentitiesOnly yes
  LogLevel FATAL
```
