# Agreed Architecture

## Repository Responsibilities

- dotw-almalinux10wsl → WSL / AlmaLinux host bootstrap
- vagrant → VM lifecycle management
- dotw-ansible → infrastructure configuration (roles + playbooks)
- platformctl → main orchestration brain

## Execution Model

- platformctl calls ansible-playbook directly
- no orchestration wrappers in dotw-ansible

## dotw-ansible Structure

dotw-ansible/
  inventories/
  playbooks/
    base.yml
    k8s.yml
    okd.yml
  roles/
    common/
    k8s/
    okd/

## Scope

- configure Vagrant labs
- configure Kubernetes clusters
- configure OKD clusters
- runs from WSL control node (AlmaLinux)
cd ../
