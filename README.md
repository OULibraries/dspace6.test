# Ansible playbook for linux infrastructure

## Notes

* Requires Ansible 2x
* Requires boto + aws credentials in the "default" boto profile
* Requires secrent Ansible Vault passphrase.
* Includes [ec2.py](http://docs.ansible.com/ansible/intro_dynamic_inventory.html#example-aws-ec2-external-inventory-script) for dynamic inventory
* Uses Ansible vault for all vars files.
* EC2 instances are spun up using the ssh crentials specified in the first element of the users var array.  See hosts/group_vars/all/vault.yml

## Install system dependencies to get started

# Windows 10

Install [Bash on Ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide), then follow Ubuntu steps.

# Fedora
```
sudo dnf install -y git gcc openssl-devel python-devel python-pip redhat-rpm-config
```

# Ubuntu
```
sudo apt-get install -y git gcc libffi-dev libpython-dev libssl-dev python-concurrent.futures python-dateutil python-pip

```

On any system, you may want to change the text editor that ansible-vault calls. To do so set the EDITOR enviornment var by your preferred method.

## Make sure you have local bin paths in your PATH
~/.bashrc should have something along the lines of:

```
PATH=$PATH:$HOME/.local/bin:$HOME/bin
export PATH
```

## Installation
* Configure git for ansible vault
```
git config --global diff.ansible-vault.textconv "ansible-vault view"
```
* Clone this repo to a local folder
* Upgrade pip and install pip dependencies
```
pip install --user --upgrade setuptools
pip install --user --upgrade pip
pip install --user -r requirements.txt

# Touch ansible logfile                            
```                                                
mkdir -p log && touch log/ansible.log              
```                                                
* Install Ansible roles                            
```                                                
ansible-galaxy install -r requirements.yml --force 

# To run your playbook against your dspace6.test server                            
```                                                
ansible-playbook /playbooks/dspace6.yml --limit dspace6.test.sok.ec2.internal
```


