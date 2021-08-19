# Ansible Lab

## Install Ansible

1.Install Asible with pip

```bash
sudo python get-pip.py
sudo python -m pip install ansible
```

2.Check ansible version

```bash
ansible --version
```

## Create a Server with Vagrant

1.Install VirtualBox

```bash
sudo apt install virtualbox virtualbox-ext-pack
```

1.Install Vagrant

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install vagrant
```

2.Create a directory and add a CentOS 7.x 64-bit ‘box’ using the vagrant box add command:

```bash
vagrant box add geerlingguy/centos7
```

3.Create a default virtual server configuration using the box you just downloaded

```bash
vagrant init geerlingguy/centos7
```

4.Boot your CentOS server

```bash
vagrant up
```

5.Open the Vagrantfile that was created when we used the vagrant init command earlier. Add the following lines just before the final ‘end’

```ruby
#Provisioning configuration for Ansible.
config.vm.provision "ansible" do |ansible|
ansible.playbook = "playbook.yml"
end
```

## Create a Playbook

1.Create an playbook yaml file in the same directory as the Vagrantfile

```yaml
---
- hosts: all
  become: yes
  tasks:
  - yum: name=ntp state=present
  - service: name=ntpd state=started enabled=yes
  ```

This is a simple example

2.Let’s run the playbook on our VM. Make sure you’re in the same directory as the Vagrantfile and new playbook.yml file, and enter

```bash
vagrant provision
```

3.Cleaning up

```bash
vagrant destroy
```
