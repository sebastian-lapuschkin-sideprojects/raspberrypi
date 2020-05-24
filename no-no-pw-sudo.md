By default, the `sudo` command on raspbian does not ask for verification via password, which can lead to some stupid and undesirable situations.
I therefore change the default password, andre-enable the password request by openining and editing `/etc/sudoers.d/010_pi-nopasswd`:

Type
```
sudo passwd
```
and then type and verify your new password.
Now disable the no-password-policy for sudo'ers with
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
