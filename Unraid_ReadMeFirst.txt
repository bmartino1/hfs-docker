Welcome to HFS3 as a docker image on unraid.

This (HTTP Files Server) HFS may require some aditional setup.

By Default, the Template is shipes to work in docker bridge mode.
It is recomend to run this in a MacVlan Custom (eth0, br0, bond0) with its own IP Address.

Due to the Docker templatle set to bridge mode this will share Unraid IP and Port.
Please click "Advance" toggle at the top and the "Show more settings ..." at the bottom to review and edit your choice for HFS VFS http and Https port
1 Variable "HFS_" set the port in the docker config at launche. The other varibale is unraid Docker Network to allow that port for its Use

Default settings have the http port set to the alternative port 8080 and https port set to 60443
you will then be able to access HFS VFS system viat http://UnRaiadIP:8080/ or https://UnRaidIP:60443/
The admin interface is accessible at path: http://[IP]:[PORT:8080]/~/admin/

At first startup you will either neet to make a custom self signed Cert. it is recomend to use the option within HFS Admin interface.
please click on
