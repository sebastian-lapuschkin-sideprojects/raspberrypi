# RaspberryPi4@home
Here I keep track of the setup and config steps on raspberry pi hardware in use at home

## OS
Below setup is based on [raspbian buster](https://www.raspberrypi.org/downloads/raspbian/), with desktop (without recommended software). Just follow the instructions on the website to create a bootable sd-card.

## Disabling no-password-policy for sudoers
Because, let's be honest, this is just dangerous. See [no-no-pw-sudo.md](no-no-pw-sudo.md) 

## Changing the hostname
I like to name my hosts after bread (because good bread is awesome). My raspi4 will therefore be named `panino`.
see [hostname.md](hostname.md) for detailed steps.

## Using the RasPI as DHCP and DNS server and network-wide ad-blocker

To increase control over my local network, I will use the RasPI to take over the tasks of a DHCP and DNS server from the cheap wifi router my ISP provides.
To this end, I install [pi-hole](https://pi-hole.net/) as a DHCP- and DNS server on the RasPI, to whitelist and blacklist ad/malware/suspicious/timesink domains to my liking. The installation of pi-hole is straight forward, and explained in [pi-hole.md](pi-hole.md).



To this end, the RasPi will be assigned a fixed IP address (for both the `eth0` and `wlan0` interfaces). See [fixed-ip.md](fixed-ip.md) for details.

Thereafter, I install [pi-hole](https://pi-hole.net/) as a DHCP- and DNS server on the RasPI, to whitelist and blacklist ad/malware/suspicious domains to my liking.

disable DHCP of router

### CONTINUE HERE. DINNER IS READY


## Auto-mounting and sharing an external disk
TODO. hd-idle to save energy and prolong life expectancy of  disk
