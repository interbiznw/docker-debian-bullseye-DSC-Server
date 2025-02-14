# Debian Bullseye in Docker optimized for Java DSC Server  (https://sites.google.com/site/mppsuite/downloads/dscserver-2) 

This Container is a full Debian Bullseye Xfce4 Desktop environment with a noVNC webGUI and all the basic tools pre-installed.

This Container also has Java installed and the latest release of DscServer (Java) Installed and Launches on every startup. ( https://sites.google.com/site/mppsuite/downloads/dscserver-2 )

Container boots really fast and java user settings are stored in /debian/.config/ and persisted on each start of the container.


## Run example
```
docker run --name Debian-DSC-Server -d \
    -p 8080:8080 \
    -p 4025:4025 \
    --net=bridge \
    --env 'ROOT_PWD=superstrongpassword' \
    --env 'CUSTOM_RES_W=1280' \
    --env 'CUSTOM_RES_H=1024' \
	--env 'UID=99' \
	--env 'GID=100' \
    --env 'UMASK=000' \
    --env 'DATA_PERM=770' \
	--volume /mnt/debian-bullseye:/debian \
    --restart=unless-stopped \
    --shm-size=2G \
	interbiznw/debian-bullseye-dsc-server:latest
```

### Webgui address: http://[SERVERIP]:[PORT]/vnc.html?autoconnect=true


-------------------------------------------------------------------------------------------------------------------------------------


You also can reverse proxy this container with nginx or apache (for an example look at the end of the page).

**ROOT ACCESS:** 1. Open up your WebGUI 2. Open up a terminal 3. Type in 'su' 4. Type in your password that you've set (no screenoutput is shown if you type in passwords in Linux) 5. Press Enter 6. You should now be root.

**Storage Note:** All things that are saved in the container should be in the home or a subdirectory in your homefolder, all files that are store outside your homefolder are not persistant and will be wiped if there is an update of the container or you change something in the template.



## Env params
| Name | Value | Example |
| --- | --- | --- |
| DATA_DIR | Home folder | /debian |
| ROOT_PWD | Please choose a strong root password | superstrongpassword |
| CUSTOM_RES_W | Your preferred screen width | 1280 |
| CUSTOM_RES_H | Your preferred screen height | 1024 |
| UID | User Identifier | 99 |
| GID | Group Identifier | 100 |
| UMASK | User file permission mask for newly created files | 000 |
| DATA_PERM | Data permissions for main storage folder | 770 |


