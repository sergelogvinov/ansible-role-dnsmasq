# Ansible role dnsmasq
Configure dnsmasq

## Install

```shell
ansible-galaxy role install git+https://github.com/sergelogvinov/ansible-role-dnsmasq.git,main
```

## Usage

```ini
# inventory file

[servers]
server-1          ansible_host=1.2.3.1
```


```yaml
# hosts/server-1.yaml

dnsmasq_configs: ["proxmox"]
dnsmasq_interfaces: ["vmbr0"]
```

```yaml
# values.yaml

- hosts: servers
  roles:
    - ansible-role-dnsmasq
```
