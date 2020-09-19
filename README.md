# Proxy client setup (Ansible Role)

[![Galaxy Quality](https://img.shields.io/ansible/quality/50801?style=flat&logo=ansible)](https://galaxy.ansible.com/monolithprojects/http_proxy_client)
[![Role version](https://img.shields.io/github/v/release/MonolithProjects/ansible-http_proxy_client)](https://galaxy.ansible.com/monolithprojects/http_proxy_client)
[![Role downloads](https://img.shields.io/ansible/role/d/50801)](https://galaxy.ansible.com/monolithprojects/http_proxy_client)
[![GitHub Actions](https://github.com/MonolithProjects/ansible-http_proxy_client/workflows/molecule%20test/badge.svg?branch=master)](https://github.com/MonolithProjects/ansible-http_proxy_client/actions)
[![License](https://img.shields.io/github/license/MonolithProjects/ansible-http_proxy_client)](https://github.com/MonolithProjects/ansible-http_proxy_client/blob/master/LICENSE)

This Ansible role will setup HTTP/HTTPS/FTP Proxy client in the Linux system (/etc/environment), Advanced Package Tool (APT) and Docker service.

**Note:** This Ansible role can run eather befor or after the Docker service is installed.

## Requirements

* Role works on most Linux distributions

* Weekly tested on:
  * CentOS/RHEL 7,8
  * Debian 9,10
  * Fedora 31,32
  * Ubuntu 16,18,20

* Root privilegies

* Ansible 2.6+.

## Role Variables

This is a copy from `defaults/main.yml`

```yaml
# Set the Proxy server address value (i.e. http://1.2.3.4:3128)

## Addresses excluded from the traffic via Proxy
no_proxy: "localhost,127.0.0.1"

# Proxy server address for HTTP traffic
# http_proxy: <address>

# Proxy server address for HTTPS traffic
# https_proxy: <address>

# Proxy server address for FTP traffic
# ftp_proxy: <address>

# Exclude environment settings from the setup
exclude_env: no

# Exclude apt from the setup
exclude_apt: no

# Exclude Docker services from the setup
exclude_docker: no
```

## Example Playbook

In this example the Ansible role will setup HTTP Proxy in the system environment, the Docker and exclude APT proxy setup.

```yaml
---
- name: Setup Proxy
  hosts: all
  user: ansible
  become: yes
  vars:
    - http_proxy: http://1.2.3.4:567
    - exclude_apt: yes
  roles:
    - role: monolithprojects.http_proxy_client
```

In this example the Ansible role will setup HTTP/HTTPS/FTP Proxy in the system environment, in APT and Docker service.

```yaml
---
---
- name: Setup Proxy
  hosts: all
  user: ansible
  become: yes
  vars:
    - http_proxy: http://1.2.3.4:567
    - https_proxy: http://1.2.3.4:567
    - ftp_proxy: http://1.2.3.4:567
  roles:
    - role: monolithprojects.http_proxy_client
```

## What is missing

* Proxy setup for yarn

## License

MIT

## Author Information

Created in 2020 by Michal Muransky
