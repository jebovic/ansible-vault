Vault
======

[![Build Status](https://travis-ci.org/jebovic/ansible-vault.svg?branch=master)](https://travis-ci.org/jebovic/ansible-vault) [![Ansible Galaxy](https://img.shields.io/badge/galaxy-jebovic.vault-blue.svg?style=flat)](https://galaxy.ansible.com/jebovic/vault)

Install and configure vault

This role is a part of my [OPS project](https://github.com/jebovic/ops), follow this link to see it in action. OPS provides a lot of stuff, like a vagrant file for development VMs, playbooks for roles orchestration, inventory files, examples for roles configuration, ansible configuration file, and many more.

Compatibility
-------------

Tested and approved on :

* Debian jessie (8+)
* Ubuntu Trusty (14.04 LTS)
* Ubuntu Xenial (16.04 LTS)

Dependencies
------------

This role depends on [jebovic.supervisor](https://github.com/jebovic/ansible-supervisor) role to be fully functional

Role Variables
--------------

```yaml
# Consul installation configuration
vault_dep_packages:
  - unzip
vault_install_dir: /usr/local/bin
vault_bin_path: "{{ vault_install_dir }}/vault"
vault_tarball_url: https://releases.hashicorp.com/vault/0.6.4/vault_0.6.4_linux_amd64.zip
vault_tmp_full_path: /tmp/vault_0.6.4_linux_amd64.zip
vault_config_dir: /etc/vault/conf.d
vault_data_dir: /var/vault

# Vault configuration
vault_http_port: 8200
vault_backends: []
vault_listeners: []
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
     - { role: jebovic.vault }
     - { role: jebovic.supervisor }
```

Example : config
----------------

```yaml
# Use Consul backend and listent on localhost:8200
vault_backends:
  consul:
    address: '"127.0.0.1:{{ consul_http_port }}"'
    path: '"vault"'

vault_listeners:
  tcp:
    address: '"127.0.0.1:{{ vault_http_port }}"'
    tls_disable: 1
```

Tags
----

* vault_config : only update config and restart service

License
-------

MIT

Author Information
------------------

Jérémy Baumgarth https://github.com/jebovic
