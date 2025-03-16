Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------
Default variables can be found in defaults/main.yml
```yaml
kubeadm_init_parameters: "--skip-phases=addon/kube-proxy"

kube_version: "1.31.2"
# Дополнительные имена для которых будет действителен сертификат api-сервера (пригодится при пробрасывании api наружу)
certExtraSANs:
  - <your domain>
# Kube-proxy/cni
service_cidr: "10.233.0.0/18"
pod_network_cidr: "10.233.64.0/18"

# calico
# Пока установка cni не автоматизирована указать нужно только инкапсуляцию
# One of: IPIP, VXLAN, IPIPCrossSubnet, VXLANCrossSubnet, None
# Work only install without eBPF
encapsulation: "IPIPCrossSubnet"
# Адрес внешнего балансировщика для api-server'а (если будет использоваться)
api_load_balancer_address: <ip address>
api_load_balancer_port: <lb port>
## HA cluser
# При установке в режиме HA используется haproxy + keepalived
# Адрес который займёт keepalived
ha_cluster_virtual_ip: 192.168.10.122
# Порт на котором будет принимать запросы haproxy
ha_cluster_virtual_port: 7443
```