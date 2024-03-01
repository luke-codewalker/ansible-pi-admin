# Network setup

Three devices powered and connected over a PoE switch to the router:

- Pi 3 running Pi Hole
- Pi 4 8GB as k3s control node
- Pi 4 4GB as k3s agent node

The static private IP (IPv4 and IPv6) of the Pi Hole is advertised via DHCP to
all devices. The upstream DNS server of the Pi Hole is the router. DNS queries
are resolved as follows:

Device ---> Pi Hole ---> Router ---> unknown public DNS servers

## Summarized Steps

- give Pi 3 and Pi 4 control node a static private IP
- configure Router to advertise Pi Holes IP (v4 and v6) as DNS server address
- set Router as upstream DNS in Pi Hole
- set up Local DNS entry to point `raspberrypi.local` to Pi 4's IP to keep using
  services with old "domain"
  - possibility for split DNS in the future

## Sources

- https://docs.pi-hole.net/routers/fritzbox-de/
- https://avm.de/service/wissensdatenbank/dok/FRITZ-Box-7490/165_Andere-DNS-Server-in-FRITZ-Box-einrichten/
- https://whitematter.tech/posts/https-for-homelab-internal-resources/
