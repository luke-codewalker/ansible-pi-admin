# Static IP and custom hostname

TODO intro and explanation

## Hostname

You can configure which hostname the Pi will use to register itself in the local network by editing `sudo nano /etc/hostname` and change the content to the desired hostname. Then edit `sudo nano /etc/hosts` and replace the old hostname with your new one everywhere. After that reboot the Pi and see it become available under the new name.

> Be aware that this breaks any configuration relying on the (old) hostname like your `~/.ssh/config` and these need to be updated with the new hostname

## Static private IP

TODO

## Sources
- https://www.makeuseof.com/raspberry-pi-set-static-ip/
- https://superuser.com/questions/983378/raspberry-pi-has-both-static-and-dhcp-ip-address
- https://www.tomshardware.com/how-to/static-ip-raspberry-pi
- https://www.tomshardware.com/how-to/raspberry-pi-change-hostname
- also https://chat.openai.com/ :shrug: