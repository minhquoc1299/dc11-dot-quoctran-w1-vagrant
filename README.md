## ph2-vagrant Ubuntu 22.04 (Jammy)
This build uses vagrant box [ubuntu/jammy64](https://app.vagrantup.com/ubuntu/boxes/jammy64)
Tools included in this build:
- Terraform
- Nodejs 18
- Docker - Docker Compose

Revise line 36 in ***Vagrantfile*** accordingly to your local environment.
Revise following configuration in ***playbook.yml*** accordingly to your need:
- SSH key importing: task 13
- AWS credential configuration: task 14
- bashrc alias: task 16

Build VM
```
vagrant up
```

Re-run playbook.yml
```
vagrant up --provision
```
