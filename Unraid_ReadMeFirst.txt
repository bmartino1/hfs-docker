For use with the CA Template...

Welcome to HFS3 as a Docker image on Unraid.

# Use Custom Network!
This HTTP File Server (HFS) may require some additional setup. It is recommended to run this in a MacVlan Custom (eth0, br0, bond0) with its own IP address. IPvlan will work as well. The key point is that it needs its own IP address tied to IPvlan/MacVlan Docker.

We also have an admin lock to the local network where you can set one IP address that will only have access, or allow access to the entire subnet (for example, 192.168.1.0/24). If you encounter a "forbidden" error, it is likely due to admin access being locked to a specific IP or the network not being set up correctly.

# Use Default Ports!
Regarding HFS VFS, since this is a web server, please click the "Advanced" toggle at the top and then the "Show more settings..." option at the bottom to review and edit your choice for HFS VFS HTTP and HTTPS ports. Default settings have been applied for HTTP/HTTPS ports: HTTP is set to port 80 and HTTPS is set to port 443. You will then be able to access the HFS VFS system via the assigned IP using: http://IP:80/ or https://IP:443/. The admin interface is accessible at the path: http://[IP]:[PORT:80]/~/admin/.

# First Run Permission Error?
Please note: At first startup, you may encounter an error in the Docker log. An example of the error is: %timestamp% Failed at saving config file, please ensure it is writable. Error: EACCES: permission denied, open 'config.yaml'. After the first run, please stop the Docker and set Unraid Docker Safe Permissions.

In the Unraid Terminal bash, run:
chmod -R 777 /mnt/user/appdata/rejettohfs3/

Then start the Docker again. You should now be able to access the admin interface by going to http://[IP]:[PORT:80]/~/admin/.

# Setup HTTPS Certificate!
Next, we need to create an HTTPS certificate. You can create a custom self-signed certificate. Currently, it is recommended to use the option within the HFS admin interface to create and use a self-signed certificate. The Tempalte is setup by default to use the admin interface self cert...

Please note: HFS VFS hardcodes the private key, which needs to be in .key format; the certificate can be in .pem format. Please click the "Advanced" toggle at the top and then the "Show more settings..." option at the bottom to review. A path has been created at /mnt/user/appdata/rejettohfs3/certs for your own certificate; please update the container path by hitting edit and using the default options to point to that location, updating names if necessary.

In the Unraid Terminal bash, run:
openssl req -x509 -newkey rsa:4096 -keyout /mnt/user/appdata/hfs/certs/privkey.key -out /mnt/user/appdata/hfs/certs/cert.pem -days 365 -nodes

Alternatively, it is recommended to use the HFS admin interface to create a self-signed certificate. The admin interface in the container will create files (later seen in the config folder): /home/hfs/.hfs/self.key and /home/hfs/.hfs/self.cer. Once the admin creates a self-signed certificate, please note that you may see a "Network Error." Please stop and then start the Docker to use HTTPS and the new assigned certificate.

# Setup HFS VFS Folder!
Finally, we need to set up the HFS VFS Source Disk to start sharing files. In the admin interface, click "Add Files." In the Docker template, you added a path you wanted to share; by default, it is /mnt/user. In the container, it will be read as: /app/myDisk.

With a custom IP, fixed permissions, a self-signed HTTPS certificate, and a folder added for HTTP/HTTPS file sharing, you are now ready to use the HFS VFS system.
