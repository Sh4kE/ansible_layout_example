# Ansible example structure
This repository is an example of how you could setup an ansible script repository. 
It has been described in [Ansible best practises](https://docs.ansible.com/ansible/playbooks_best_practices.html)

## Running ansible playbooks
You can either update all servers by running:
```
ansible-playbook -i testing.ini site.yml 
```


or update only a subset of servers via:
```
ansible-playbook -i testing.ini site.yml --limit dbservers
ansible-playbook -i testing.ini webservers.yml
```

## Ansible Vault ...
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
**Don't forget to add this file to youre .gitignore if you put it inside of your repository!** 