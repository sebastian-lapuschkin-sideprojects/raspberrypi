The pi-hole package can easily be installed via a single call to

```
curl -sSL https://install.pi-hole.net | bash
```

which will guide you through a shell-based graphical installation. After the installation, you will be shown an initial login password. Note that down.
Your pi-hole admin console will now be available via (assuming you set `hostname` to `panino`) [http://panino.local/admin/](http://panino.local/admin/).
where you should first change your password after logging in, and can configure all your stuff. 

Navigate to `Settings->DHCP` and `Settings->DNS` to set up the fundamentals of your network.
Also monitor `Network` from time to time, to figure out which network devices are using pi-hole as DNS and DHCP server, and which ones stubbornly avoid to do so.
The latter ones might have custom/manual DNS configurations in place.
Note that some devices may take a while to adapt to pi-hole, e.g. until their WAN lease must be renewed. Rebooting those devices will in most cases trigger a WAN lease renewal. *Any* secondary DHCP server on the network broadcasting/or alternative DNS information (be that a DHCPv6-server baked into your router you can not deactivate, as in my case, or DNS info hardcoded into some of your apps) may allow ads or blocked content to bypass your pi-hole.

Note that above call / the pi-hole installation sets up [lighttpd](https://www.lighttpd.net/) as a lightweight web server, through which you just accessed the pi-hole dashboard. Note that by default, lighttpd listens on port 80, which will cause conflicts with apache2, the web server installed and managed in context of the [nextcloud(pi) installation](nextcloudpi.md).

As you will probably interact with the pi-hole dashboard --- after a (first and occasional) setup of your black- and whitelists --- way less than with the nextcloud web interface, you should exchange the default server port for lighttpd to some other not yet reserved. Enter the following command to configuer lighttpd:

```
sudo nano /etc/lighttpd/lighttpd.conf
```

now look for 
```
server.port                 = 80
```
and replace the port value with (e.g.) `9969`. The line should now read
```
server.port                 = 9969
``` 

Now `sudo reboot` your RasPI. The pi-hole admin dashboard should shortly be available via `http://panino.local:8017/admin/`, and the installation of your nextcloud server in [nextcoudpi.md](nextcloudpi.md) should work out without conflicts.

