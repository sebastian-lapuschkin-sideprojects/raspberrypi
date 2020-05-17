unformatted. format text below

isntall nextcloud server from

https://github.com/nextcloud/nextcloudpi

by running

```
curl -sSL https://raw.githubusercontent.com/nextcloud/nextcloudpi/master/install.sh | sudo bash
```

note that since we installed pihole earlier, port 80 currently is blocked and apache2 will not be able to listen on port 80 (you migt have seen an error during installation)
in order to let nextcloud and pihole coexist, edit /etc/apache2/ports.conf for apache to listen to e.g. port 8080 instead  of 80.
also edit /etc/apache2/sites-enabled/000-default.conf accordingly. now nextcloud graphical setup is available via panino.local:8080/ . 

problem: pi.hole overwritten with apache2 default page. figure this out.

**CONTINUE/COMPLETE**
