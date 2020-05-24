The following steps will setup raspbian to automatically mount (a specific) external disk drive at a predetermined mount point.
The instructions have been adapted from [https://www.raspberrypi.org/documentation/configuration/external-storage.md](https://www.raspberrypi.org/documentation/configuration/external-storage.md)

First, let's create (or pick) a mount point, where the disk('s data) should be available from. This can in principle be any empty folder. I decided to use the generically named `/mnt/disk` for that, and create the folder with

```
sudo mkdir /mnt/disk
```

If you have not done so already, connect the disk drive to the USB (3.0, if available) port. Now list all the connected disks and partitions on the RasPI with

```
sudo lsblk -o UUID,NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL,MODEL
```

In my case, the output looks like this:
```
UUID                                 NAME        FSTYPE  SIZE MOUNTPOINT LABEL       MODEL
                                     sda                 1.8T                        Elements
47525d23-43e1-4bbc-9b87-34299502e713 └─sda1      ext4    1.8T            WD-2TB-ext4 
                                     mmcblk0            59.5G                        
6341-C9E5                            ├─mmcblk0p1 vfat    256M /boot      boot        
80571af6-21c9-48a0-9df5-cffb60cf79af └─mmcblk0p2 ext4   59.2G /          rootfs      
```

Note that the mount points `/` and `/boot` are used by the PI itself. `sda` thus is my external disk drive and `sda1` its first and only partition, which I have formatted beforehand to an `ext4` file system format. No extra file system drivers need to be installed for `ext4`.

Let us now (manually) mount the disk with `sudo mount /dev/sda /mnt/disk`
and verify the disk has been mounted successfully by listing its contents with `ls -a /mnt/disk`.
If you can see your files on the drive, or at least `.` and `..` in case the drive is empty, the disk has been mounted with success.


The command `sudo blkid` shows that `sda1` is located at `/dev/sda1`, and lists all the partition info (again):
```
/dev/mmcblk0p1: LABEL_FATBOOT="boot" LABEL="boot" UUID="6341-C9E5" TYPE="vfat" PARTUUID="ea7d04d6-01"
/dev/mmcblk0p2: LABEL="rootfs" UUID="80571af6-21c9-48a0-9df5-cffb60cf79af" TYPE="ext4" PARTUUID="ea7d04d6-02"
/dev/sda1: LABEL="WD-2TB-ext4" UUID="47525d23-43e1-4bbc-9b87-34299502e713" TYPE="ext4" PARTLABEL="WD-2TB-ext4" PARTUUID="f4567076-27be-4fef-9832-273b17c419f5"
```

Now, in order to ensure the disk is being mounted automatically on system startup, we have to configure the `/etc/fstab` file by adding the target partition's `PARTUUID` and mount point to the listed entries. From the previously called `blkid` output, we know that for `sda1`:
```
PARTUUID="f4567076-27be-4fef-9832-273b17c419f5"
```

Now call `sudo nano /etc/fstab` and enter the following line at the end of the file:
```
PARTUUID="f4567076-27be-4fef-9832-273b17c419f5" /mnt/disk ext4 defaults,auto,users,rw,nofail,x-systemd.device-timeout=10 0 0
```

Note the added `x-systemd.device-timeout=10` causes the RasPi to only wait for 10 seconds for the disk to react on bootup, instead of the default 90 seconds, which shortens the boot time of your raspberry pi considerbly should you choose to keep the drive disconnected.

Now `sudo reboot` and verify the disk auto-mounts by executing `ls -a /mnt/disk`.
If it did not work for you, make sure you used *your own data*, not mine.
