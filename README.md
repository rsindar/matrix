# Matrix Homeserver Ansible Playbook

This repository contains an Ansible playbook for deploying a **Matrix homeserver** based on [Tuwunel](https://github.com/matrix-construct/tuwunel), [Coturn](https://github.com/coturn/coturn), and [Caddy](https://caddyserver.com/).  

## Features
- Deploys **Tuwunel** (Matrix homeserver)
- Installs and configures **Coturn** for VoIP/RTC traffic
- Sets up **Caddy** as a reverse proxy with HTTPS (Let’s Encrypt)

## Requirements
- Ansible ≥ 2.12
- A fresh Linux server (1 CPU, 1GB RAM, 10GB SDD, RHEL/AlmaLinux/Rocky/Debian/Ubuntu)
- SSH access with sudo privileges
- DNS records pointing to your server
- The following network ports must be open:
    - 80/tcp
    - 443/tcp
    - 8448/tcp
    - 3478/tcp, 3478/udp
    - 5349/tcp, 5349/udp
    - 49152-65535/udp

## Usage
**Create inventory.yml:**
<pre>
---
all:
  hosts:
    matrix_server:
      ansible_host: 1.2.3.4
      ansible_user: myuser
      matrix_fqdn: my-matrix.tld
      tuwunel_reg_token: SECRET1
      turn_secret: SECRET2
</pre>
**NB! Never use not encrypted secrets in the inventory file.**
<pre>
ansible-vault encrypt_string 'SECRET1' --name 'tuwunel_reg_token'
ansible-vault encrypt_string 'SECRET2' --name 'turn_secret'
</pre>
**Run:** ansible-playbook site.yml -i inventory.yml --ask-vault-pass

## Matrix clients
- [Element Web](https://app.element.io/#/register)
- [SchildiChat](https://play.google.com/store/apps/details?id=de.spiritcroc.riotx)
- [Element Classic](https://play.google.com/store/search?q=element+classic&c=apps)

P.S. Unfortunately, both SchildiChat and Element Classic cannot create users when token-based registration is used. You should create users in Element Web or in the Admin Room.

## Todo
- [Matrix RTC/Element Call Setup](https://github.com/matrix-construct/tuwunel/blob/main/docs/matrix_rtc.md)
- Migration in to [K0s](https://k0sproject.io/)
