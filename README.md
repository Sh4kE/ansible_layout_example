# Ansible structure example like described in Ansible docs best practises

# Running ansible playbooks
You can either update all servers by running:
```
ansible-playbook -i testing.ini site.yml 
```


or update only a subset of servers via:
```
ansible-playbook -i testing.ini site.yml --limit dbservers
ansible-playbook -i testing.ini webservers.yml
```