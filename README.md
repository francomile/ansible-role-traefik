# Ansible Traefik Role

[![Lint Ansible roles](https://github.com/francomile/ansible-role-traefik/actions/workflows/ansible_lint.yml/badge.svg)](https://github.com/francomile/ansible-role-traefik/actions/workflows/ansible_lint.yml)

[![Release role to Ansible Galaxy](https://github.com/francomile/ansible-role-traefik/actions/workflows/push_to_galaxy.yml/badge.svg)](https://github.com/francomile/ansible-role-traefik/actions/workflows/push_to_galaxy.yml)

## Actions

- Install Traefik Docker
- Setup SSL (optional)

## Dependencies

- Depends on `francomile.localhost` Ansible role for setting up loopback alias interface (100.64.64.64)
- Depends on `francomile.docker` for installing Docker Engine.

## Common Usage

```yaml
roles:
  - {
    roles: francomile.traefik,
    # loopback alias requires to run netpoan role first.
    netplan_loopback_alias_ip: "100.64.64.64",
    # traefik.yml template variables
    traefik_docker_network: "traefik",
    traefik_log_level: "ERROR",
    traefik_accesslog_format: "common", # common, json, logfmt
    traefik_log_format: "common", # common, json, logfmt
    traefik_acme_staging_enabled: true, # Let's Encrypt - Staging API
    traefik_acme_production_enabled: false, # Let's Encrypt - Production API
    traefik_dashboard_enabled: false,
    traefik_dashboard_enabled_insecure: false,
    traefik_prom_metrics_enabled: true, # Enable Prometheus metrics
    traefik_redirect_to_websecure: true, # Redirect to HTTPS
    traefik_ssl_certificates_enabled: false, # Enable your own SSL certificates
    # if 'ssl_certificates_enabled: true', you will need to specify them in the below vars:
    traefik_ssl_cert: "your_ssl_cert",
    traefik_ssl_key: "your_ssl_cert_priv_key",
    traefik_certificatesresolvers_acme_email: "admin@example.com",
    # Traefik docker-compose.yaml variables
    traefik_docker_cpu: 1,
    traefik_docker_memory: "2G",
    traefik_docker_replicas: 1,
    traefik_http_port: 80,
    traefik_https_port: 443,
    traefik_image: "traefik:v2.7",
    traefik_install_dir: "/opt/traefik",
    tags: ["traefik"]
  }
```

## Run the playbook

```shell
ansible-playbook -i inventory playbook.yaml --tags "traefik"
```
