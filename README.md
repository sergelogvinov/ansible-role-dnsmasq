# Ansible role dnsmasq

Basic role to configure dnsmasq.
Very useful for router or proxmox hosts.

It setups:
* dns-cache
* dhcp-v4
* ipv6 route advertiser (if network/bridge has IPv6)

And it uses `ndppd` to proxy neighbor discovery messages.

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
dnsmasq_interfaces: ["vmbr0"] # interfaces to manage
dnsmasq_ndp: true             # proxy neighbor discovery
dnsmasq_dhcp_ranges:          # dhcp-v4 range
  vmbr0:
    from: "{{ ansible_facts['vmbr0'].ipv4.address | ansible.utils.ipmath(-51) }}"
    to:   "{{ ansible_facts['vmbr0'].ipv4.address | ansible.utils.ipmath(-31) }}"
    leasetime: 12h
```

```yaml
# values.yaml

- hosts: servers
  roles:
    - ansible-role-dnsmasq
```
