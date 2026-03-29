# Zabbix Monitoring Lab

## Requirements
- VirtualBox
- Vagrant
- Ansible

## Network
- Zabbix Appliance: 192.168.56.10
- Bastion-ansible: 192.168.56.20

## Steps

### 1. Start Bastion VM
```
vagrant up
vagrant ssh
```

### 2. Clone repository
```
sudo git clone https://github.com/sposdknl/ansible01-zbx-sxriii.git /opt/repo
cd /opt/repo
```

### 3. Install Ansible collection
```
sudo ansible-galaxy collection install community.zabbix --upgrade
```

### 4. Run playbook
```
sudo ansible-playbook -i inventory.ini -l bastion configure_servers.yml
```

### 5. Zabbix Appliance
- Import OVF from zabbix.com
- Set eth1: 192.168.56.10
- Login: Admin / zabbix

### 6. Auto-registration
- Alerts -> Actions -> Autoregistration actions
- Create action with condition: Host metadata contains linux
- Operations: Add host, Add to host group Linux servers, Link template Linux by Zabbix agent active

### 7. Verify
- Monitoring -> Hosts -> bastion should appear
- Monitoring -> Latest data -> select bastion