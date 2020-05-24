# RaspberryPi4@home
Here I keep track of the setup and config steps on raspberry pi hardware in use at home

## OS
Below setup is based on [raspbian buster](https://www.raspberrypi.org/downloads/raspbian/), with desktop (just in case), without recommended software. Just follow the instructions on the website to create a bootable sd-card, using the [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/) for your OS. In order to enable ssh right out of the box, create an empty file called `ssh` in the `/boot`partition on the sd card you just created. 

### Basics
In your first ssh session, enter `sudo raspi-config` and first enter option `8` to update the raspi-config tool if possible. Then, enter option `1` to change the default password for user `pi`. Interact as instructed. Optionally enter menu points `2` to change the hostname connect to your local WiFi. Exit the configuration tool, reboot and re-connect via `ssh`.


### Disabling no-password-policy for sudo'ers
Because, let's be honest, this is just dangerous. See [no-no-pw-sudo.md](no-no-pw-sudo.md) 

### Changing the hostname
I like to name my hosts after bread (because good bread is awesome). My raspi4 will therefore be named `panino`. If this has not been done in section "Basics" above, 
see [hostname.md](hostname.md) for detailed steps.


## Network management
To increase control over my local network, I will use the RasPI to take over the tasks of a DHCP and DNS server from the cheap wifi router my ISP provides.

### Setting up the Pi-Hole as DHCP and DNS server and network-wide ad-blocker
To this end, I install [pi-hole](https://pi-hole.net/) as a DHCP- and DNS server on the RasPI, to whitelist and blacklist ad/malware/suspicious/timesink domains to my liking. The installation of pi-hole is straight forward, and explained in [pi-hole.md](pi-hole.md).

### Static network settings
Next, I disabled the DHCP-server functionality in my WiFi router (which should be possible in any router provided by ISPs) via the router's web interface, and configured static network settings for the RasPi for it to take control over the local network. See [static-network-settings.md](static-network-settings.md) for details.

Now reboot the machine using `sudo reboot`.

## Data and Storage management
One key task intended for the RasPi is the role as a "cloud" platform for data management, e.g. providing access to files and  media centralized for the whole local network.

### Auto-mounting and sharing an external disk
As a high capacity storage solution, I'd like to permanently connect (and automatically mount) a [portable USB hard disk](https://shop.westerndigital.com/de-de/products/portable-drives/wd-elements-portable-usb-3-0-hdd#WDBUZG0010BBK-WESN).
In short, this requires the creation of a mount point, and the configuration of the `/etc/fstab` file. The necessary steps can be found in [external-disk.md](external-disk.md).

The external disk I have connected and had at my disposal was a conventional HDD with physically moving parts, i.e. a spinning disk. In order to minimize energy consumption and prolong the life expectancy of the drive, I have set the disk up to enter an "idle" status after a certain time of inactivity. See [disk-standby.md](disk-standby.md) for details.

### FUTURE CONSIDERATIONS.
Nextcloud. consider rebooting once a week or so using cron jobs: also caching and logging of pi-hole
