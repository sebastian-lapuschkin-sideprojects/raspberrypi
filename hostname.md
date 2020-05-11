(1) replace the contents of /etc/hostname with your hostname of choice, e.g. "raspberrypi" to "panino"

`sudo nano /etc/hostname`

(2) now replace the known host name for the loopback address in /etc/hosts with "panino"

`sudo nano /etc/hosts`

the file's contents should now look like this:
```
127.0.0.1       localhost
::1             localhost ip6-localhost ip6-loopback
ff02::1         ip6-allnodes
ff02::2         ip6-allrouters

127.0.1.1       panino
127.0.0.1       panino
```

(3) set the host name using hostnamectl
 `sudo hostnamectl set-hostname panino`

(4) restart the pi
 `sudo reboot`

there are other ways to change the hostname, but this one works, too.

