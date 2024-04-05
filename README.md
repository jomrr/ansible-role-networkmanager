# ansible-role-networkmanager

![GitHub](https://img.shields.io/github/license/jomrr/ansible-role-networkmanager) [![Build Status](https://travis-ci.org/jomrr/ansible-role-network-manager.svg?branch=main)](https://travis-ci.org/jomrr/ansible-role-network-manager)

**Ansible role for installing networkmanager and configuring connections.**

First development version of the role.

> Currently only installation and nmcli config is possible.
> Reboot is not done via role.

## Supported Platforms

- Alpine
- Archlinux
- CentOS
- Debian
- Fedora
- OpenSuse Leap, Tumbleweed
- OracleLinux
- Ubuntu

## Requirements

Ansible 2.9 or higher.

## Variables

Variables and defaults for this role.

### defaults/main.yml

```yaml
# The role is disabled by default, so you do not get in trouble.
# Checked in tasks/main.yml which uses a tasks block if enabled.
networkmanager_role_enabled: false

# Specify additional packages to install for NetworkManager plugin:
# EXAMPLE: Install vpnc plugin on Debian for connection to AVM FritzBox VPN
# networkmanager_plugins:
#   - network-manager-vpnc
networkmanager_plugins: []

# Configuration via nmcli module, takes list of dicts, for keys see:
# https://docs.ansible.com/ansible/latest/collections/community/general/nmcli_module.html
# ATTENTION: Always specify "state: present|absent", as ansible nmcli requires it.
# ATTENTION2: The nmcli module is not idempotent...
# EXAMPLE:
# networkmanager_nmcli:
#   - type: ethernet
#     conn_name: dummy0
#     dns4: 192.168.200.1
#     dns4_search: my.domain.test
#     ifname: enps3
#     ip4: 192.168.200.25/24
#     gw4: 192.168.200.1
#     state: present
networkmanager_nmcli: []
```

## Dependencies

None.

## Example Playbook

```yaml
---
# role: ansible-role-networkmanager
# file: site.yml

- hosts: all
  become: true
  gather_facts: true
  vars:
    networkmanager_role_enabled: true
  roles:
    - role: ansible-role-networkmanager
```

## License and Author

- Author:: [jomrr](https://github.com/jomrr/)
- Copyright:: 2021, [jomrr](https://github.com/jomrr/)

Licensed under [MIT License](https://opensource.org/licenses/MIT).
See [LICENSE](https://github.com/jomrr/ansible-role-networkmanager/blob/master/LICENSE) file in repository.

## References

- [ArchWiki](https://wiki.archlinux.org/title/NetworkManager)
- [GNOME Developer](https://developer.gnome.org/NetworkManager/stable/NetworkManager.conf.html)
