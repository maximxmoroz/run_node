# Preview

 This script do few things

[Install Requirements](#InstallRequirements) for Bostrom node: firewall, GPU drivers, etc.  
[Install Node](#InstallNode) with Snapshot download  
[Install Snapshot](#InstallSnapshot) (Only if Bostrom node already working)
## Preparing the local environment

### Install ansible on your local pc/laptop

```brew install ansible```

### Add some info to inventories/hosts.ini

To ansible_host add Domain or IP ***address*** of your server \
To ansible_user add ***name of user*** from your server \
To ansible_become_password add ***password*** from your server

### Add your ssh key with access to server to ssh-agent localy

```ssh-add ~/.ssh/id_rsa```

### ***WARNING***:
If you decide not to add a personal ssh key to the agent, then during the execution of scripts you may be asked for a password

<p id="InstallRequirements"></p>

## Install Requirements

Start script with command:  

```bash
ansible-playbook -i inventories/hosts.ini install_requirements.yaml 
```

<p id="InstallNode"></p>

## Install Node

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="pull_container"
```

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="snapshot_download"
```
### Your script should successfully complete at the snapshot_download step

You can check the download status using the command on your server:

```bash
tmux attach -t snapshot_download
```

To exit Tmux without interrupting the download process, use command: ```Ctrl+B then D```

### Be careful, some steps are run under Tmux on your server and must be run with separate commands presented below

This decision was made due to the fact that ansible can break connections with servers due to unstable Internet, use of VPN, etc.

### After the snapshot has downloaded successfully, use the following command to unpack the archive

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="untar"
```

It will create another tmux process on your server

```bash
tmux attach -t snapshot_extract
```

To exit Tmux without interrupting the download process, use command: ``` Ctrl+B then D ```

### After successfully unpacking the snapshot, run the task that adds peer addresses and restart container

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="peers"
```

<p id="InstallSnapshot"></p>

## Install Snapshot

If you already have a  node and you want to download and install a new snapshot then use the following commands

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="download"
```

Run the following command only if you are sure that the snapshot has been downloaded

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="untar"
```

Run the following command only if you are sure that the snapshot has been successfully untar into the ***~/.cyber*** folder

```bash
ansible-playbook -i inventories/hosts.ini install_node.yaml --tags="start_bostrom"
```
