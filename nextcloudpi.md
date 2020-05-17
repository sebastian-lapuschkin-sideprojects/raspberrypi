Let us now install a nextcloud server on the RasPi, by using a preconfigured installer for Raspian/RaspberryPi, called [nextcloudpi](https://github.com/nextcloud/nextcloudpi).
Run
```
curl -sSL https://raw.githubusercontent.com/nextcloud/nextcloudpi/master/install.sh | sudo bash
```

After the installation process completes, you will be shown the following information:
```
First: Visit https://192.168.0.10/  https://nextcloudpi.local/ (also https://nextcloudpi.lan/ or https://nextcloudpi/ on windows and mac)
to activate your instance of NC, and save the auto generated passwords. You may review or reset them
anytime by using nc-admin and nc-passwd.
Second: Type 'sudo ncp-config' to further configure NCP, or access ncp-web on https://192.168.0.10:4443/
Note: You will have to add an exception, to bypass your browser warning when you
first load the activation and :4443 pages. You can run letsencrypt to get rid of
the warning if you have a (sub)domain available.
```

You can safely ignore the `nextcloudpi` hostname, which due to above message should give you access to the nextcloud interface.
As we have installed nextcloud(pi) on top of an existing raspbian installation, and have picked our own hostname in [hostname.md](hostname.md), you will be able to reach the activation page of the nextcloud server in your browser via `
https://192.168.0.10` (or `https://192.168.0.10/activate`) and `https://panino.local` (or `https://panino.local/activate`).

Now use your browser to navigate to `https://192.168.0.10/activate`.
You will be greeted with a very blue web page, containg two sets of information, which reads:
```
NextCloudPi Activation

Your NextCloudPi user is ncp

Your NextCloudPi password is VWL4nNbiIKz7H+5P5H8U1oJC8ziFAUAA9HhTJXfzAYw
  
Save this password in order to access to the NextCloudPi web interface at https://nextcloudpi.local:4443

This password can be changed using 'nc-passwd'


-----------------------------------------------------------------------------------------------------------

Your NextCloud user is ncp

Your Nextcloud password is nT+OH9BsKc8/fPpLDGlagPlffH7AqZSy8laO/z543PI

Save this password in order to access NextCloud https://nextcloudpi.local

This password can be changed from the Nextcloud user configuration
```
Again, ignore the mentionings of `nextcloudpi.local` and mentally replace it with the true URL `panino.local`.

Note down the user credentials for each point of access.
The data at the top of the page is relevant for the admin page of your nextcloud server (reachable via `https://192.168.0.10:4443` or in a moment* via `https://panino.local:4443`).
The data at the bottom of the page is relevant for your initial user login.
The data at the top of the page is relevant for the admin page of your nextcloud server (reachable via `https://192.168.0.10` or in a moment* via `https://panino.local`).
 Then press the "Activate" at the bottom of the page, which will transport you to the nextcloud admin page, where you will login with the admin user credentials. Feel free to ignore the wizard for now. 
 
Now, let's get back to the terminal, and activate `panino.local` as a "trusted domain" from which the nextcloud server should be reachable. Enter
```
sudo nano /var/www/nextcloud/config/config.php
```
and modify 
```
  'trusted_domains' =>                                                                       
  array (                                                                                    
    0 => 'localhost',                                                                        
    11 => '95.168.153.44',                                                                   
    1 => '192.168.0.10',                                                                     
    5 => 'nextcloudpi.local',                                                                
    7 => 'nextcloudpi',                                                                      
    8 => 'nextcloudpi.lan',                                                                                                                                       
  ), 
```
to
```
  'trusted_domains' =>                                                                       
  array (                                                                                    
    0 => 'localhost',                                                                                                                                           
    1 => '192.168.0.10',
    2 => '192.168.0.11'
    5 => 'panino.local',                                                                
    7 => 'panino',                                                                      
    8 => 'panino.lan',                                                                                                                                       
  ), 
```
and save the file. This will for now (until we decide otherwise at some point) allow access to the nextcloud from within your local network.

Now use your browser to access [https://panino.local:4443](https://panino.local:4443) to setup the database and data storage.

**CONTINUE HERE**
