# Fresh install

1. Go Root:

```
sudo su
```

2. Install Ansible:

```
sudo apt install -y software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install -y ansible
```

3. Git Clone Repo:

```
git clone https://github.com/maximxmoroz/ansible-script.git &&
cd ansible-script
```

4. Setup Docker with Ansible:

```
ansible-playbook docker.yaml
```

5. Setup Nvidia drivers:

```
ansible-playbook nvidia.yaml
```

6. Reboot the system for the changes to take effect:

```
sudo reboot
```

7. Install Nvidia container runtime for docker:

```
ansible-playbook nvidia-container.yaml
```
