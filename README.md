# Install ansible on your local pc/laptop
```brew install ansible```
# Add some info to inventories/hosts.ini
To ansible_host add Domain or IP address of your server
To ansible_user add name of user from your server
To ansible_become_password add password from your server
# Add your ssh key to ssh-agent localy
```ssh-add ~/.ssh/id_rsa```
# Start script
```ansible-playbook -i inventories/hosts.ini install.yaml```