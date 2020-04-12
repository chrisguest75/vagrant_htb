# README.md
A demonstration of how to use Vagrant to bring up VMs on virtualbox for HTB testing.
  
## TODO
1. Build a template vagrantfile

## Prequisites
[Vagrant Setup](https://www.vagrantup.com/intro/getting-started/project_setup.html)

### Installation of Vagrant and Ansible
Install on MacOS 

Tested on vagrant: 2.2.7 & ansible 2.9.2

```sh
brew install ansible
brew cask install vagrant
```

Install on Linux
```sh
apt install ansible
apt install vagrant
```

Install role dependencies
```sh
ansible-galaxy role list
ansible-galaxy install nickjj.docker
ansible-galaxy install gantsign.oh-my-zsh 
```

Creating a new default Vagrantfile
```sh
vagrant init hashicorp/bionic64
```

### Build VMs
NOTE: If provision is not working it may be because you have an old version of vagrant 
```sh
vagrant up
vagrant provision
```

```sh
vagrant up --provider virtualbox --provision
```

## Reboot VMs
```sh
vagrant reload
```

## Remove VMs
```sh
vagrant destroy
```

## Connect VMs
Vagrant supports ssh directly to the box
```sh
vagrant ssh
```

But if you would rather use the ssh tool
```sh
ssh -i ./.vagrant/machines/default/virtualbox/private_key -l vagrant -o StrictHostKeyChecking=no -p 2222 127.0.0.1
```

We can also use VSCode to remote-ssh and edit files on the VM
```sh
code --install-extension ms-vscode-remote.remote-ssh
```

```sh
vagrant ssh-config
``` 
then copy the output to ssh-config

```
Host ubuntu-htb
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /Users/user/Code/scratch/vagrant_htb/ubuntu-htb/.vagrant/machines/default/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL
```

## SSH Tunneling
NOTE: Work out how to get this working.
If hosting a service on a port tunnel if to host machine. 
```
ssh -i ./.vagrant/machines/default/virtualbox/private_key -l vagrant -o StrictHostKeyChecking=no -p 2222 -L 8080:127.0.0.1:8080 -N 127.0.0.1 -v
```

## Troubleshooting

