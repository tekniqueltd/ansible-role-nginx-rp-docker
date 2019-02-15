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
            nginx_rp_docker_proxy_config:
              - name: app1
                path: /
                backend: [
                  "server1:8080"
                ]
                configs: |
                  proxy_set_header Host $host;
                  proxy_set_header X-Real-IP $remote_addr;
                  proxy_set_header X-Forwarded-Port  $server_port;
                  proxy_set_header Host $host;
                  proxy_set_header X-Real-IP $remote_addr;
                  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                  proxy_set_header X-Forwarded-Proto $scheme;
              - name: grafana
                path: /
                backend: [
                  "server2:3000",
                  "server3:3000"
                  ]
                configs: |
                  proxy_http_version 1.1;
                  proxy_pass_header   Server;
                  proxy_set_header X-Forwarded-Port  $server_port;
                  proxy_set_header Host $host;
                  proxy_set_header X-Real-IP $remote_addr;
                  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                  proxy_set_header X-Forwarded-Proto $scheme;
          }


## Add as a submodule to your playbook repo

    git submodule add https://github.com/tekniqueltd/ansible-role-nginx-rp-docker.git roles/nginx-rp-docker
