# Ansible-Role-Scalelite

## Table of content

- [Ansible-Role-Scalelite](#ansible-role-scalelite)
  - [Table of content](#table-of-content)
  - [Example host_vars file](#example-host_vars-file)

## Example host_vars file

```yaml
---
docker_postgres:
  user: "admin"
  # REQUIRED
  password: ""
  # YOU MUST SET THE PASSWORD HERE AS WELL EXAMPLE `admin:admin`
  url: "postgres://admin:YOU_NEED_TO_CHANGE_THIS@postgres:5432/scalelite?pool=5"

docker_scalelite:
  repo: "blindsidenetwks"
  tag: "v1"
  recording_dir: "/mnt/scalelite-recordings/var/bigbluebutton"

docker_nginx:
  ssl: true
  url_host: "{{ inventory_hostname }}"

docker_redis:
  url: "redis://redis:6379"

docker_scalelite_api:
  # REQUIRED
  secret_key_base: "d42985d38feb585577a8966239aebcc1"
  # REQUIRED
  loadbalancer_secret: "dedf24bce87891c1644d9b8903ec6d67"
  # REQUIRED - Can be multible separated by : Example "Secret1:Secret2:Secret3"
  loadbalancer_secrets: "80a1605cb33dd216c284b1e36aeb41f7"
  redis_url: "redis://redis:6379"
  url_host: "{{ inventory_hostname }}"

docker_letsencrypt:
  email: "{{ certbot_admin_email }}"
  # 0 no staging | 1 staging
  staging: 0

# REQUIRED
certbot_admin_email: certbot@domain.tld
certbot_auto_renew_minute: "20"
certbot_auto_renew_hour: "5"
certbot_create_if_missing: true
certbot_create_method: standalone
certbot_create_standalone_stop_services:
  - docker
certbot_certs:
  # REQUIRED
  - email: certbot@domain.tld
    domains:
      - "{{ inventory_hostname }}"
```
