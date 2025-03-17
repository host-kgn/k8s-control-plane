# Role Name

The role for the control-plane configuration and k8s-cluster initialization.

# Requirements

# Role Variables
## Kubeadm configuration
Default variables can be found in `defaults/main.yml`
### InitConfiguration

`kubeadm_init_parameters` - [see documentation](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-init/#options) <br>
`kube_version` - Role tested with 1.31.2 <br>
`certExtraSANs` - List of additional domains for the API server. Useful when accessing the API server through an external load balancer. <br>

---

### ClusterConfiguration

`service_cidr` - subnet for services <br>
`pod_network_cidr` - subnet for pods
> **Note**: The specific subnets depend on the CNI (Container Network Interface) plugin you use.

---

`api_load_balancer_address` <br>
`api_load_balancer_port` <br>
```