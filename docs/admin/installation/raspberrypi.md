---
sidebar_position: 3
id: raspberry-pi
title: Installation on Raspberry Pi
---

# OpenCloud on Raspberry Pi

⚠️ **Note:** This guide shows how to set up **OpenCloud on a Raspberry Pi**. 
The installation is **only recommended for use in a local network**. 
If you want to make OpenCloud accessible over the internet, you will need to set up **additional security measures** such as a firewall, SSL certificates and secure authentication.
This requires advanced network and server knowledge. 
Without these safeguards, your instance could be vulnerable to attack.

---

## 1.1 Hardware requirements

- Minimum Raspberry Pi 4B with at least 4 GB RAM connected via LAN or WLAN
- Micro SD card with at least 32 GB storage space
- External hard disk or USB-Stick (optional) for additional storage space

## 1.2 Install operating system

- Install OS  
  A very detailed and understandable guide is available at:  
  [Raspberry Pi Getting Started](https://pimylifeup.com/raspberry-pi-getting-started/)
- SSH must be activated
<img src={require("./img/raspberrypi/ssh-activate.png").default} alt="activate ssh" width="500"/>

- If the Raspberry Pi is to be connected to WLAN, the login data for the WLAN must be entered.

## 1.3 Connecting with SSH

Start the Raspberry Pi with the SD card and connect via SSH.  
The IP for this can be viewed in your router.

<img src={require("./img/raspberrypi/ip-router.png").default} alt="find ip from raspberry-pi in router" width="500"/>

### Establish connection via SSH:
```sh
ssh pi@YOUR-IP
```

After the first login, you should change the password for security reasons:
```sh
passwd
```

## 1.4 Installing Docker and Docker Compose

Detailed installation instructions for docker can be found here:  
[Install Docker on Raspberry Pi](https://pimylifeup.com/raspberry-pi-docker/)

- Perform update and upgrade

```sh
sudo apt update && sudo apt upgrade -y
```
- Install Docker via Script

```sh
curl -fsSL test.docker.com -o get-docker.sh && sh get-docker.sh
```

- Add current user to the Docker Group

```sh
sudo usermod -aG docker ${USER}
```
- Check if it`s running:

```sh
groups ${USER}
```
<img src={require("./img/raspberrypi/docker-user-check.png").default} alt="Check docker user" width="500"/>

- Reboot the Raspberry Pi to let the changes take effect

```sh
sudo shutdown -r now
```
- Install Docker-Compose

```sh
sudo apt install docker-compose
```

- Check the installation

```sh
docker-compose --version
```
<img src={require("./img/raspberrypi/docker-compose-check.png").default} alt="Check docker-compose" width="500"/>


## 1.5 Clone OpenCloud respository

```sh 
git clone https://github.com/opencloud-eu/opencloud.git
``` 


## 1.6 Start the docker compose setup

```sh 
docker compose up opencloud traefik
```



## 1.7 Change the deployment

Go to the deployment folder and open the `.env` file with e.g. nano 

```sh 
cd opencloud/deployments/examples/opencloud_full
``` 
```sh 
nano .env
```

When you added an external hard disk or USB-Stick for the storage, you need to enable the `OC_DATA_DIR` variable and change the path to your storage

<img src={require("./img/raspberrypi/change-env-for-storage.png").default} alt="Check docker-compose" width="500"/>


Here it is `/mnt/data`

You can also enable the `DEMO_USERS` when you set them to `true` or can change the `ADMIN_PASSWORD`

## 1.5 Mount external hard disk or USB-Stick (optional)

- Find your external hard disk or USB-Stick

```sh
lsblk
```
<img src={require("./img/raspberrypi/find-external-hd.png").default} alt="Check docker-compose" width="500"/>

- Format the drive to ext4 filesystem

```sh
sudo mkfs.ext4 PATH-TO-DRIVE -L DATA
```
PATH-TO-DRIVE is in this example `/dev/sda1` so the command would be

```sh
sudo mkfs.ext4 /dev/sda1 -L DATA
```
<img src={require("./img/raspberrypi/format-drive.png").default} alt="Check docker-compose" width="500"/>

- Add entry in fstab for automatic mounting when restarting

  - open fstab with sudo
```sh
  sudo nano /etc/fstab
```
  - add following line in the fstab file

```sh 
LABEL=DATA /mnt/data ext4 auto,defaults 0 0
```

  - create the `/mnt/data` directory and give the user 1000 access

```sh 
sudo mkdir -p /mnt/data
```
```sh 
sudo chown -R 1000:1000 /mnt/data
```

  - mount the drive automatically 
```sh 
sudo mount -a
```  

Maybe you get following error

<img src={require("./img/raspberrypi/error-mounting.png").default} alt="Check docker-compose" width="500"/>

then please perform the reccomended command 

```sh 
systemctl daemon-reload
``` 
and try to mount again.

192.168.2.52 opencloud.opencloud.test
192.168.2.52 traefik.opencloud.test
192.168.2.52 collabora.opencloud.test
192.168.2.52 onlyoffice.opencloud.test
192.168.2.52 wopiserver.opencloud.test
192.168.2.52 mail.opencloud.test
192.168.2.52 companion.opencloud.test
192.168.2.52 minio.opencloud.test
192.168.2.52 cloud.opencloud.test