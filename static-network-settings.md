In order to let the RasPI sucessfully act as (its own and) the network's DHCP and DNS server, we have to configure its network interface. Specifically, we want to ensure that the RasPI will have a static IP address, and uses *itself* as DNS. Open the file `/etc/dhcpcd.conf` and edit its contents. Look for `Example static IP configuration` and uncomment/modify the data below to

```
# Example static IP configuration:
interface eth0
static ip_address=192.168.0.10/24             # set the IP of the ethernet adapter
static ip6_address=fd51:42f8:caae:d92e::ff/64
static routers=192.168.0.1                    # determine your network's router as standard gateway
static domain_name_servers=127.0.0.1          # let the RasPI use itself as DNS.

interface wlan0                               # repeat for the WiFi adapter
static ip_address=192.168.0.11/24
static routers=192.168.0.1
static domain_name_servers=127.0.0.1
```

Note that setting the RasPIs DNS to `127.0.0.1` will prevent `/etc/resolv.conf` being overwritten on every reboot, which might otherwise interfere with the pi-hole's blocklist update procedures.
