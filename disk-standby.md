In order to reduce the energy footprint of the RasPI, and to prolong the life expectancy of the connected but infrequently used HDD storage, I wish to power down the disk after it just sits there and spins unproductively for a certain amount of time.
For this purpose, I plan to deploy [hd-idle](http://sourceforge.net/projects/hd-idle), which however is not available as a pre-built package (yet).

At first, I ensure the required build tools are installed and available by calling
```
sudo apt-get install build-essential debhelper -y
```

Then download, extract, build debian package and install in that order. Ignore the warning that signing of the package has failed.
```
wget http://sourceforge.net/projects/hd-idle/files/hd-idle-1.05.tgz
tar -xvf hd-idle-1.05.tgz
cd hd-idle
dpkg-buildpackage
sudo dpkg -i ../hd-idle_*.deb
cd ..
```

Next, configure the configuration file of hd-idle for hd-idle to run on boot, and to shut down any idle disk after a desired interval. Call `sudo nano /etc/default/hd-idle` and adapt the following values in the beginnig and the end of the file to
```
START_HD_IDLE=true
[...]
HD_IDLE_OPTS="-i 300 -l /var/log/hd-idle.log"
```
Here, the value after `-i` specifies the time in seconds after which an idle disk will be put into standby mode. Note that this configuration applies to *all* disks. If you wish to target specific disks, you can target a drive with `-a` after each  `-i`, e.g. as
```
HD_IDLE_OPTS="-i 0 -a sda -i 300 -a sdb -i 900"
```
Consider removing the downloaded/extracted folder with `rm -r hd-idle`.
Now call `sudo service hd-idle restart` or `sudo reboot` to enable hd-idle as a service.
