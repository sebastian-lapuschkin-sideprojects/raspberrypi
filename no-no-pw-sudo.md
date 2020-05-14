By default, the `sudo` command on raspbian does not ask for verification via password, which can lead to some stupid and undesirable situations.
I therefore re-enable the password request by openining and editing `/etc/sudoers.d/010_pi-nopasswd`:

```
sudo nano /etc/sudoers.d/010_pi-nopasswd
```

The only content of that file should be:

```
pi ALL=(ALL) NOPASSWD: ALL
```

Change it to:

```
pi ALL=(ALL) PASSWD: ALL
```
