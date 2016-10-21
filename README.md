# Ansible example structure
This repository is an example of how you could setup an ansible script repository. 
It has been described in [Ansible best practises](https://docs.ansible.com/ansible/playbooks_best_practices.html)

## What is Ansible
* Configuration Management tool
* It communicates with remote machines over SSH
* configured via ini files
* Can be run from any machine with Python 2.6 or 2.7 installed (Currently)
* Managed nodes need Python 2.4 or later

## Ansible Language

### Modules
* (also referred to as “task plugins” or “library plugins”) are the workers in ansible
* Ansible ships with a number of modules that can be executed directly on remote hosts ([List of all Modules](https://docs.ansible.com/ansible/list_of_all_modules.html))
* Users can also write their own modules ( in python <3 ), but you probably don't need to. 

### Playbooks
* are Ansible’s configuration, deployment, and orchestration language
* describe a policy you want your remote systems to enforce
* can and should be idempotent (can be run several times without changing anything)

###  Inventories
Ansible works against multiple systems in your infrastructure at the same time. It does this by selecting portions of systems listed in Ansible’s inventory file, which defaults to being saved in the location `/etc/ansible/hosts`. You can specify a different inventory file using the `-i <path>` option on the command line.

* contain groups of servers to tell ansible, which servers your system is made up of
* written in the ini file format
* servers may be added to multiple groups
* groups of groups possible as well (for building a tree of servers)

### Roles
* Structure defines file usage (Convention over Configuration)
  * See this repositories structure
  * [Role Structure](https://docs.ansible.com/ansible/playbooks_best_practices.html#directory-layout)

## Running ansible

### Running a module ad hoc
```
ansible scriptclub -m ping
ansible all -a "/bin/echo hello"
ansible -i inventory_file webservers -m service -a "name=httpd state=restarted"
```

### Running playbooks
You can either provision all servers by running:
```
ansible-playbook -i testing.ini site.yml 
```

or provision only a subset of your servers via:
```
ansible-playbook -i testing.ini site.yml --limit dbservers
ansible-playbook -i testing.ini webservers.yml
```

4. Ansible Vault ...
... is a secure Key-Value store, which allows keeping sensitive data such as passwords or keys in an encrypted file. This vault file can then be distributed or placed in source control.

To create a new encrypted data file, run the following command:
```
ansible-vault create secure.yml
```
It will ask you for a password.

And to edit it afterwards run:
```
ansible-vault edit secure.yml
```

To run a playbook, which contains vault-encrypted variables, you can either tell ansible to ask you for the password:
```
ansible-playbook -i testing.ini site.yml  --ask-vault-pass
```

Or you create a file with that password and pass it to ansible:
```
cat your_secret_password > ~/.vault_pass
ansible-playbook -i testing.ini site.yml --vault-password-file ~/.vault_pass
```
**Don't forget to add this file to your .gitignore if you put it inside of your repository!** 

