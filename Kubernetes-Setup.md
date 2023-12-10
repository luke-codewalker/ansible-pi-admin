# Kubernetes (k3s) setup

To cluster my Raspberry Pis together I use Kubernetes and more specifically "lightweight kubernetes" https://k3s.io/. When installing k3s on a Pi you first need to decide whether this Pi will be the control plane for the cluster or an agent/worker node that is managed by the control server.

## Steps

1. configure the Pis memory: `sudo nano /boot/cmdline.txt` and add ` cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1` (space is separator!)
2. Control plane
    - SSH into Pi and run install script `curl -sfL https://get.k3s.io | sh -`
    - Copy out kubeconfig to local machine from `/etc/rancher/k3s/k3s.yaml` to `~/.kube/config`
    - Test connection with `kubectl`
3. Install on agent node
    - Todo


## Sources
- https://docs.k3s.io/quick-start
- https://www.padok.fr/en/blog/raspberry-kubernetes
