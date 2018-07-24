Ansible Role: nginx-rp-docker
----------------------

Ansible role that deploys a nginx reverse proxy container using docker and docker-compose

## Supported Operating Systems

- Debian 9+
- Ubuntu 16.04+ (untested)

## Requirements

- Ansible 2.4+ (on execution host)
- Docker 17+ (on remote host)

## Role Variables

See `./defaults/main.yml` for configurable variables and their defaults

## Example playbook

    ---
    - name: Example play
      hosts: all
      roles:
        - { role: nginx-rp-docker }

## Example playbook (with some optional vars set)

    ---
    - name: Example play with some optional vars set
      hosts: all
      roles:
        - { role: nginx-rp-docker,
            nginx_rp_docker_image_version: 1.15.0,
            nginx_rp_docker_backends: [
              "server1:8080",
              "server2:8080"
            ]
          }

## Add as a submodule to your playbook repo

    git submodule add https://github.com/tekniqueltd/ansible-role-nginx-rp-docker.git roles/nginx-rp-docker
