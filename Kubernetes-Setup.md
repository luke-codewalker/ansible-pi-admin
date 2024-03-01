# Kubernetes (k3s) setup

To cluster my Raspberry Pis together I use Kubernetes and more specifically
"lightweight kubernetes" https://k3s.io/. When installing k3s on a Pi you first
need to decide whether this Pi will be the control plane for the cluster or an
agent/worker node that is managed by the control server.

## Steps

1. configure the Pis memory: `sudo nano /boot/cmdline.txt` (or
   `/boot/firmware/cmdline.txt` on Pi4) and add
   `cgroup_enable=cpuset cgroup_enable=memory cgroup_memory=1` (space is
   separator!)
2. Control plane
   - SSH into Pi and run install script `curl -sfL https://get.k3s.io | sh -`
   - Copy out kubeconfig to local machine from `/etc/rancher/k3s/k3s.yaml` to
     `~/.kube/config`
   - Test connection with `kubectl`
3. Install on agent node
   > To install additional agent nodes and add them to the cluster, run the
   > installation script with the K3S_URL and K3S_TOKEN environment variables.
   > Here is an example showing how to join an agent:
   > `curl -sfL https://get.k3s.io | K3S_URL=https://myserver:6443 K3S_TOKEN=mynodetoken sh -`
   > Setting the K3S_URL parameter causes the installer to configure K3s as an
   > agent, instead of a server. The K3s agent will register with the K3s server
   > listening at the supplied URL. The value to use for K3S_TOKEN is stored at
   > /var/lib/rancher/k3s/server/node-token on your server node.

## Tips

- uninstall k3s on control plane by running `/usr/local/bin/k3s-uninstall.sh`

## Sources

- https://docs.k3s.io/quick-start
- https://www.padok.fr/en/blog/raspberry-kubernetes
