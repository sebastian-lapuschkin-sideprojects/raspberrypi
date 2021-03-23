## Creating a Samba shared folder

In this section, we set up a network-shared folder for easy file sharing in the local network.
This will be a public folder usable by anyone.


First, the samba package needs to be installed:

```
sudo apt update && sudo apt-get install samba -y
```
I did not need to install and configure samba on my own, as the installation of nextcloudpi already took care of that.


Make sure the value for `workgroup` is set (ie sth. is written behind the ` = `). The configuration file can be edited via
```
sudo nano /etc/samba/smb.conf
```
Also make sure to create a resource for sharing, such as
```
[Shared on Pi]
comment = Public Share on Local Net
path = /SMB_SHARE
create mask = 0777
directory mask = 0777
writeable = yes
browseable = yes
public = yes
guest ok = yes
```
Note here that we created the network shared folder at te directory root as a symbolic link to an external HDD drive, via
```
sudo ln -s /SMB_SHARE [target_path]
```


Now test the created profile for errors with
```
sudo testparm
```

Before we start the server, you’ll want to set a samba password. I have no idea if this is vital or not. Just following and piecing together some guides to make it work on raspbian.
```
sudo smbpasswd -a pi
```

In order to make our above configured resource discoverable on the local net, check the status of the samba service (optional) and restart it.
```
sudo systemctl restart smbd
sudo systemctl status smbd
```

That's it. your local-network-wide public samba share should now be accessible to all users.
