# Storage

## Hardware

To enable persistent storage in my cluster I have added a USB stick to each Pi.
Before I can add PVs and PVCs in k3s I need to mount the USB sticks as they are
not automatically mounted:

- ssh into device
- create a mount point like so: `sudo mkdir /media/usb`
- list all attached storage with `sudo blkid` and look for the USB stick (in my
  case upper USB 3.0 port was `/dev/sda1`)
- format the USB drive to a filesystem Longhorn can use
  `sudo mkfs.ext4 /dev/sda1`
- mount the device: `sudo mount /dev/sda1 /media/usb`

## Longhorn

To use all the storage from any node in the cluster I installed Longhorn and
configured the USB sticks as the only drives (via the UI).

### Issues with Longhorn I had to solve

- the drives really need to be in one of the supported file formats!
- thoroughly check the installation requirements and fulfill them on every node
  - I had to install `open-iscsi` on the Pis
  - Executing the official requirements check script helped:
    `curl -s https://raw.githubusercontent.com/longhorn/longhorn/v1.6.0/scripts/environment_check.sh | bash`
- the Longhorn UI has an
  [issue](https://github.com/longhorn/longhorn/issues/1745) that allows only '/'
  to be used as ingress path. I simply added a CNAME record in Pi Hole to use
  the subdomain longhorn.domain.local
- as I only have two drives in my cluster all volumes would be "unhealthy" as
  they couldn't reach their desired replica count which is 3 by default. To
  adjust this edit the config map of the longhorn storage class with
  `kubectl edit configmap longhorn-storageclass -n longhorn-system` and adjust
  `parameters.numberOfReplicas`

## Sources

- https://longhorn.io/docs/1.6.0/deploy/install/#installation-requirements
- https://rpi4cluster.com/k3s/k3s-storage-setting/#add-storage01
- https://www.computerhilfen.de/info/usb-stick-oder-festplatte-am-raspberry-pi-nutzen.html
- https://longhorn.io/docs/1.6.0/deploy/install/install-with-helm/
- https://www.reddit.com/r/kubernetes/comments/126mgbc/longhorn_help_unable_to_attach_volume_to_mounted/
