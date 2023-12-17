# Power saving

I can save power and avoid network conflicts [like this one](https://gist.github.com/luke-codewalker/25ede894edde3f4a33043757bafeb079) by turning of WiFi for the Pi. Additionally I can disable Bluetooth.

Edit the boot config file'
```
sudo nano /boot/config.txt
```

and add or edit

```
[all]  
dtoverlay=disable-wifi
dtoverlay=disable-bt
```

and finally `sudo reboot` to apply the changes.


## Sources
- https://pimylifeup.com/raspberry-pi-disable-wifi/