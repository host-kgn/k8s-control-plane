# Role Name

The role for the control-plane configuration and k8s-cluster initialization.

# Requirements
You can use this `requirements.yml`:
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

# Role Variables
## Kubeadm configuration
Default variables can be found in `defaults/main.yml`
### InitConfiguration

`kubeadm_init_parameters` - [see documentation](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/#options) <br>
`kube_version` - Role tested with 1.31.2 <br>
`certExtraSANs` - List of additional domains for the API server. Useful when accessing the API server through an external load balancer. <br>

---

### ClusterConfiguration
> **Note:** The specific subnets depend on the CNI (Container Network Interface) plugin you use.

`service_cidr` - subnet for services <br>
`pod_network_cidr` - subnet for pods <br>
`api_load_balancer_endpoint` - endpoint of external loadbalncer for Kube-API.<br>
