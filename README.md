# RaspberryPi4@home
Here I keep track of the setup and config steps on raspberry pi hardware in use at home

## OS
Below setup is based on [raspbian buster](https://www.raspberrypi.org/downloads/raspbian/), with desktop (just in case), without recommended software. Just follow the instructions on the website to create a bootable sd-card, using the [Raspberry Pi Imager](https://www.raspberrypi.org/downloads/) for your OS. In order to enable ssh right out of the box, create an empty file called `ssh` in the `/boot`partition on the sd card you just created. 

### Basics
In your first ssh session, enter `sudo raspi-config` and first enter option `8` to update the raspi-config tool if possible. Then, enter option `1` to change the default password for user `pi`. Interact as instructed. Optionally enter menu points `2` to change the hostname connect to your local WiFi. Exit the configuration tool. Now type `nano .bashrc` and enable some QoL features as the `ll` alias, to your liking.
Conclude with
```
sudo apt update && sudo apt upgrade -y && sudo reboot
```
in order to bring the system up to date.
Reconnect via `ssh` to proceed with the steps below.


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

### Installing Nextcloud
Now, let's install Nextcloud(pi) and use it as an easy to access file server to the local network. Follow the instructions in [nextcloudpi.md](nextcloudpi.md).

### Setting up a public network shared folder using Samba
In order to use the pi as a hub for sharing files conveniently, we set it up as a sambanserver in [samba.md](samba.md)

### Enabling hitch-less streaming playback on the raspberry Pi 4b
Just follow [streaming.md](streaming.md)

### Slightly overclock the Pi for even smoother media playback.
Hitches and freezes are now minimized, but we can still safely crank up the performance a bit. The process is quite easy, and the results are (not) noticable. Have a look at [overclock.md](overclock.md)
