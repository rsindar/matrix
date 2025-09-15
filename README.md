# Matrix Homeserver Ansible Playbook

This repository contains an Ansible playbook for deploying a **Matrix homeserver** based on [tuwunel](https://github.com/matrix-construct/tuwunel), [Coturn](https://github.com/coturn/coturn), and [Caddy](https://caddyserver.com/).  

## Features
- Deploys **Tuwunel** (Matrix homeserver)
- Installs and configures **Coturn** for VoIP/RTC traffic
- Sets up **Caddy** as a reverse proxy with HTTPS (Let’s Encrypt)
- Configurable via group vars and inventory

## Requirements
- Ansible ≥ 2.12
- A fresh Linux server (Red Hat family)
- SSH access with sudo privileges
- DNS records pointing to your server
- The following network ports must be open:
    - 443/tcp
    - 8448/tcp
    - 3478/tcp, 3478/udp
    - 5349/tcp, 5349/udp
    - 49152-65535/udp

## Usage
ansible-playbook -i matrix_server, site.yml
