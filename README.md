# ansible-role-hashicorp-proxy

Ansible role for setup and configure hashicorp-proxy.

## Requirements

- Systemd on the target host
- Firewalld

## Variables 

| Variable | Type | Default | Comment |
| ------ | ------ | -------  | ---------- |
| hp_user | string | hashiproxy | System user |
| hp_home_dir | string | /opt/hashiproxy | Home directory |
| hp_oncalendar | string | 02:00 | Scheduled time to run sync |
| hp_source_host | string | https://hc-mirror.express42.net/ | Mirror source |
| hp_mirror_host | string | https://repo.platform.tatar.ru/repository/hashicorp/ | Mirror repo (Nexus) |
| hp_mirror_username | string | '' | Mirror repo username |
| hp_mirror_password | string | '' | Mirror repo password |
| hp_tmp_dir | string | /tmp/mirror | Temporary directory |
| hp_fs_repo | string | https://github.com/s-starostin/hashicorp-proxy.git | Fileserver git repo url |
| hp_add_open_ext_port | bool | False | Configure firewalld to open fs port |
| hp_fs_ssl_enabled | bool | False | Enable SSL |
| hp_fs_ssl_check_hostname | bool | False | Strict check SSL hostname |
| hp_fs_ssl_server_cert | string | server-cert.pem | SSL server certificate |
| hp_fs_ssl_server_cert_key | string | server-key.pem | SSL server key |
| hp_fs_host | string | localhost | Fileserver host |
| hp_fs_port | int | 3000 | Fileserver port |
| hp_fs_directory | int | files/repo.platform.tatar.ru/repository/hashicorp | Fileserver docroot |
| hp_fs_providers_subpath | int | /providers/ | Fileserver providers endpoint |
| hp_fs_routes | dict | [See example below](#routes-example) | Fileserver provider routes | 

## Routes example

```
hp_fs_routes:
  registry.terraform.io/hashicorp/ad: terraform-provider-ad
  registry.terraform.io/hashicorp/archive: terraform-provider-archive
  registry.terraform.io/hashicorp/aws: terraform-provider-aws
  registry.terraform.io/hashicorp/awscc: terraform-provider-awscc
  registry.terraform.io/hashicorp/azuread: terraform-provider-azuread
  registry.terraform.io/hashicorp/azurerm: terraform-provider-azurerm
  registry.terraform.io/hashicorp/azurestack: terraform-provider-azurestack
  registry.terraform.io/hashicorp/boundary: terraform-provider-boundary
  registry.terraform.io/hashicorp/cloudinit: terraform-provider-cloudinit
  registry.terraform.io/hashicorp/consul: terraform-provider-consul
  registry.terraform.io/hashicorp/dns: terraform-provider-dns
  registry.terraform.io/hashicorp/external: terraform-provider-external
  registry.terraform.io/hashicorp/google: terraform-provider-google
  registry.terraform.io/hashicorp/google-beta: terraform-provider-google-beta
  registry.terraform.io/hashicorp/googleworkspace: terraform-provider-googleworkspace
  registry.terraform.io/hashicorp/hcp: terraform-provider-hcp
  registry.terraform.io/hashicorp/hcs: terraform-provider-hcs
  registry.terraform.io/hashicorp/helm: terraform-provider-helm
  registry.terraform.io/hashicorp/http: terraform-provider-http
  registry.terraform.io/hashicorp/kubernetes: terraform-provider-kubernetes
  registry.terraform.io/hashicorp/kubernetes-alpha: terraform-provider-kubernetes-alpha
  registry.terraform.io/hashicorp/local: terraform-provider-local
  registry.terraform.io/hashicorp/nomad: terraform-provider-nomad
  registry.terraform.io/hashicorp/null: terraform-provider-null
  registry.terraform.io/hashicorp/oci: terraform-provider-oci
  registry.terraform.io/hashicorp/opc: terraform-provider-opc
  registry.terraform.io/hashicorp/oraclepaas: terraform-provider-oraclepaas
  registry.terraform.io/hashicorp/random: terraform-provider-random
  registry.terraform.io/hashicorp/salesforce: terraform-provider-salesforce
  registry.terraform.io/hashicorp/template: terraform-provider-template
  registry.terraform.io/hashicorp/terraform: terraform-provider-terraform
  registry.terraform.io/hashicorp/tfe: terraform-provider-tfe
  registry.terraform.io/hashicorp/time: terraform-provider-time
  registry.terraform.io/hashicorp/tls: terraform-provider-tls
  registry.terraform.io/hashicorp/vault: terraform-provider-vault
  registry.terraform.io/hashicorp/vsphere: terraform-provider-vsphere
  registry.terraform.io/hashicorp/hashicups: terraform-provider-hashicups
```

## Playbook example

```
---
- hosts: all
  become: True
  vars:
      hp_mirror_username: 'test'
      hp_mirror_password: 'test'
  roles:
    - ansible-role-hashicorp-proxy
```