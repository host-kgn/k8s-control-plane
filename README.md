# k8s-control-plane

The role for the control-plane configuration and k8s-cluster initialization.

## Requirements
Example of `requirements.yml`:
```yaml
collections:
  # Install a collection from Ansible Galaxy.
  - name: community.general
    version: ">=7.0.0"
    source: https://galaxy.ansible.com
  - name: ansible.posix
    version: ">=1.5.4"
    source: https://galaxy.ansible.com
```

## Role Variables
### Kubeadm configuration
Default variables can be found in `defaults/main.yml`
#### InitConfiguration

`kubeadm_init_parameters` - [see documentation](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/#options) <br>
`kube_version` - Role tested with 1.32.2 <br>
`certExtraSANs` - List of additional domains for the API server. Useful when accessing the API server through an external load balancer. <br>

---

#### ClusterConfiguration
> **Note:** The specific subnets depend on the CNI (Container Network Interface) plugin you use.

`service_cidr` - subnet for services <br>
`pod_network_cidr` - subnet for pods <br>
`api_load_balancer_endpoint` - endpoint of external loadbalncer for Kube-API. Used <br>

### Inventory examples
#### Multimaster
```yaml
k8s_masters:
  hosts:
    km-1:
      ansible_ssh_host: 192.168.0.10
    km-2:
      ansible_ssh_host: 192.168.0.11
    km-3:
      ansible_ssh_host: 192.168.0.12
k8s_workers:
  hosts:
    kw-1:
      ansible_ssh_host: 192.168.0.13
    kw-2:
      ansible_ssh_host: 192.168.0.14
    kw-3:
      ansible_ssh_host: 192.168.0.15
k8s_cluster:
  children:
    k8s_masters:
    k8s_workers:
```
When installing multiple masters, an external load balancer for kube-api will be required. The load balancer's endpoint must be specified in the `api_load_balancer_endpoint` variable.

---
#### Single-master
```yaml
k8s_masters:
  hosts:
    km-1:
      ansible_ssh_host: 192.168.0.10
k8s_workers:
  hosts:
    kw-1:
      ansible_ssh_host: 192.168.0.11
    kw-2:
      ansible_ssh_host: 192.168.0.12
    kw-3:
      ansible_ssh_host: 192.168.0.13
k8s_cluster:
  children:
    k8s_masters:
    k8s_workers:
```