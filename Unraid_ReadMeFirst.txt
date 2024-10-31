*For use with the CA Template...
Welcome to HFS3 as a docker image on unraid.

# Use Custom Network!
This (HTTP Files Server) HFS may require some aditional setup.
It is recomend to run this in as MacVlan Custom (eth0, br0, bond0) with its own IP Address.
IPvlan will work as well. The point I that it needs it own IP address that is tied to ipvlan/MacVlan Docker...

We also have a admin lock to local netowrk you can set 1 ip address that will only have access or the entire subnet as example 192.168.1.0/24
If you gett error forbiden it is due to admin access being locked to a ip or the network is not set...

# Use Default Ports!
Regarding HFS VFS as this is a Web server.
Please click "Advance" toggle at the top and the "Show more settings ..." at the bottom to review and edit your choice for HFS VFS HTTP and HTTPS port...
Default settings have been applied for http/https ports. THey are set to http port 80 and  https port 443....
you will then be able to access HFS VFS system via the assigned IP you give it http://IP:80/ or https://IP:443/
The admin interface is accessible at path: http://[IP]:[PORT:80]/~/admin/

# Frist Run Permission error?
Please Note:
At first startup you may encounter an error in the docker log:
Example of error : %timestamp% Failed at saving config file, please ensure it is writable. Error: EACCES: permission denied, open 'config.yaml'
After first run please stop the docker and set Unraid Docker Safe Permissions.

Unraid Terminal bash
chmod -R 777 /mnt/user/appdata/rejettohfs3/

Then start the docker again. You should now be able to access the admin interface by goin to http://[IP]:[PORT:80]/~/admin/

# Setup HTTPS Certificate!
Next we need to make a HTTPS Certificate.
You can make a custom self signed Cert. ATM it is recommened to use the option within HFS Admin interface to make and use a self signed cert.
*Please note HFS VFS is Hard Code the Private key need to be as .key the certificate can be .pem ...
Please click "Advance" toggle at the top and the "Show more settings ..." at the bottom to review
Please not a path was made to /mnt/user/appdata/rejettohfs3/certs to use your own please update to the continer path by hitting edit and use default options to point to that location update names if any...

Unraid Terminal bash
openssl req -x509 -newkey rsa:4096 -keyout /mnt/user/appdata/hfs/certs/privkey.key -out /mnt/user/appdata/hfs/certs/cert.pem -days 365 -nodes

Otherwise -Recommended- Please use The HFS Admin interface to create a self-signed Certificate
the admin interface in the continer will make a file(latter seen in the config folder): /home/hfs/.hfs/self.key and /home/hfs/.hfs/self.cer
once the admin make a self cert please note that you may see "Network Error" Please stop then start the docker to use https and the new assigned certificate.

# Setup HFS VFS Folder!
Last we need to set up the HFS VFS Source Disk to start sharing Files.
In the Admin Interface click add files. in the Docker tempatle you added a path you wanted to share by default it is /mnt/user
in the container it will be read as: /app/myDisk

with Permission A custom IP, Permissions Fixed, A Https Self Signed Cert, and Folder added for HTTP/HTTPS file sharing You are now ready to use HFS VFS system.
