# POE+ HAT
I'm powering the Pi via the official [PoE+ HAT](https://www.raspberrypi.com/products/poe-plus-hat/) (**P**ower **o**ver **E**thernet **H**ardware **A**ttached on **T**op). This comes with a fan for cooling the obstructed CPU which is known to be overly aggressive and have an annoying whining sound. 
To combat this you can edit `/boot/config.txt` to tell the Pi to only turn on the fan at higher temperatures:

```
# PoE Hat Fan Speeds
dtparam=poe_fan_temp0=50000
dtparam=poe_fan_temp1=60000
dtparam=poe_fan_temp2=70000
dtparam=poe_fan_temp3=80000
```

Using the `stress` utility you can also ramp up the CPU usage and then measure the temperature and check how fast the fan turns on:

```
sudo apt-get install stress # install utility
stress -c 4 -t 30s # stress test all 4 CPU cores for 30 seconds
vcgencmd measure_temp # print out the CPU temperature
```


## Sources
- https://www.jeffgeerling.com/blog/2021/taking-control-pi-poe-hats-overly-aggressive-fan
- https://github.com/raspberrypi/linux/issues/2715#issuecomment-769405042
- https://core-electronics.com.au/guides/stress-testing-your-raspberry-pi/