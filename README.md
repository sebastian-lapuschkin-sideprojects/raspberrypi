# RaspberryPi4@home
Here I keep track of the setup and config steps on raspberry pi hardware in use at home

## OS
Below setup is based on [raspbian buster](https://www.raspberrypi.org/downloads/raspbian/), with desktop (without recommended software).

## Changing the hostname
I like to name my hosts after bread (because good bread is awesome). My raspi4 will therefore be named `panino`.
see [hostname.md](hostname.md) for detailed steps.

## Using the RasPI as DHCP and DNS server and network-wide ad-blocker
To increase control over my local network, I will use the RasPI to take over the tasks of a DHCP and DNS server from the cheap wifi router my ISP provides.
To this end, the RasPi will be assigned a fixed IP address (for both the `eth0` and `wlan0` interfaces). See [fixed-ip.md](fixed-ip.md) for details.

Thereafter, I install [pi-hole](https://pi-hole.net/) as a DHCP- and DNS server on the RasPI, to whitelist and blacklist ad/malware/suspicious domains to my liking.

### CONTINUE HERE. DINNER IS READY


## Auto-mounting and sharing an external disk
TODO
