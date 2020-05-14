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

Next, I disabled the DHCP-server functionality in my WiFi router (which should be possible in any router provided by ISPs) via the router's web interface, and configured static network settings for the RasPi for it to take control over the local network. See [static-network-settings.md](static-network-settings.md) for details.

Now reboot the machine using
```
sudo reboot
```

## CONTINUE HERE: Auto-mounting and sharing an external disk
TODO. hd-idle to save energy and prolong life expectancy of  disk
