# Ansible Operator SDK Demo

This project is the beginnings of a demo using the Ansible Operator Framework SDK

This requires MiniKube (already assuming you have a hypervisor installed)

```bash
$ brew install kubectl
$ brew cask install minikube
```

## First, MemcacheD Notes:

The role for memcached has quickstart notes that are confirmed to work. ( https://github.com/operator-framework/operator-sdk-samples/tree/master/ansible/memcached-operator )

### Quickstart

1. Start [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) (e.g. `minikube start`)

    We will be using the `default` namespace, and the `default` account

1. Deploy the Memcached Ansible Operator

    * Create the Memcached Ansible Operator RBAC and Service Account files
        ```bash
        $ kubectl create -f deploy/service_account.yaml
        $ kubectl create -f deploy/role.yaml
        $ kubectl create -f deploy/role_binding.yaml
        ```

    * Create the Memcached Ansible Operator Custom Resource Definitions (CRD)
        ```bash
        kubectl create -f deploy/crds/cache_v1alpha1_memcached_crd.yaml
        ```
    * Deploy the Memcached Ansible Operator
        ```bash
        kubectl create -f deploy/operator.yaml
        ```

1. Create the Memcached Ansible Operator Custom Resource (CR)

    ```bash
    kubectl create -f deploy/crds/cache_v1alpha1_memcached_cr.yaml
    ```

### Uninstall

To uninstall the Deployment and the Memcached Ansible Operator, run the following commands

1. Uninstall
    ```bash
    kubectl delete -f deploy/crds/cache_v1alpha1_memcached_cr.yaml
    ```
1. Uninstall Memcached Ansible Operator
    ```bash
    kubectl delete -f deploy/operator.yaml
    ```

Verify that the all pods created with the deployment are being `terminated` and are deleted

## MCRouter Notes:

Using this as the base role template: https://github.com/entercloudsuite/ansible-mcrouter

### Details

Installs mcrouter on Ubuntu 16.04 (Xenial)

#### Requirements

This role requires Ansible 2.4 or higher.

#### Role Variables

The role defines most of its variables in `defaults/main.yml`:

#### Example Playbook

```yaml
---
- name: run the main role
  hosts: all
  roles:
    - role: ansible-mcrouter
      mcrouter_address: localhost:11213
  become: yes
```

