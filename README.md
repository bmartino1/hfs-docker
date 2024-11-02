# HFS 3
This is not my work, This has been edited to work for my needs and the needs of the Unraid Comunity...
Please support the Orginal Project. https://github.com/rejetto/hfs
This is a Fork from Offical Docker Repo: https://github.com/damienzonly/hfs-docker

## Other Environment HFS Variables
This docker image doesn't have any specific env. Every env starting with `HFS_` will be passed to HFS.
Read [How to modify configuration](https://github.com/rejetto/hfs/blob/main/config.md#how-to-modify-configuration) page to learn more about how envs work.

## Docker Volumes and Mounts
You can mount as many volumes as you wish in docker to persist the file storage, but keep in mind that if you want to persist HFS configurations as well you **must** mount a volume that points to the `cwd` of HFS (which you can override with `HFS_CWD` env).
The default hfs cwd of the container is `/home/hfs/.hfs`

## Unraid Run container
1. Install Docker Compose Plugin
2. Git clone the repo
```
cd /mnt/user/appdata
git clone https://github.com/bmartino1/hfs-docker.git
cd hfs-docker
chmod -R 777 *
```
3. Unraid Web Ui > Docker Tab
   - Add New Stack > Click Advance and set the path: /mnt/user/appdata/hfs-docker

4. Edit Stack > Compse File and fix / update volume mounts for your instance.
   - Fix Networking As you should use this docker with your exisiing MacVlan/IPVlan set to your br0/boind0/eth0 the interface as outlined in the compose file

5. Start the docker by clicking compose up in the WebUI

   - Setup HFS by adding Https Certs(ATM setup will use self signed certs created at first launch). Then add volume to share over HFS VFS system.

   - Example command to make your own self signed certificate

```
openssl req -x509 -newkey rsa:4096 -keyout /mnt/user/appdata/hfs-docker/certs/pself.key -out /mnt/user/appdata/hfs-docker/certs/cert.pem -days 365 -nodes
```

   - Setup HFS VFS by adding the contienr path /app/myDisk to the source 
![image](https://github.com/user-attachments/assets/abec5b56-3d1c-4d1b-947c-c2160d95b728)

WIP for a docker varaible: https://github.com/rejetto/hfs/discussions/792 

6. Review HFS Support on github: https://github.com/rejetto/hfs/discussions
7. Review unraid Docker Support on Unraid: WIP (?UnRaid Forum link Comming Soon?)

##UnRaid Comunity App Store and XML
WIP
Many Thanks to Squid and GrtGbln in there help and expertisse in this matter!

CA Own repository: https://github.com/bmartino1/RejetoHFS3
WIP:
Self Hosters: 
A PR( https://github.com/selfhosters/unRAID-CA-templates/pull/531 ) has been created via repo https://github.com/bmartino1/unRAID-CA-templates
for https://github.com/selfhosters/unRAID-CA-templates

