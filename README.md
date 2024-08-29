# Wireguard-docker-setup

This repository provides instructions for running `wg-easy` using Docker. `wg-easy` is a simple and easy-to-use web interface for managing WireGuard.

## Docker Command

To run `Wireguard GUI` with Docker, use the following command:

```bash
docker run -d \
  --name=wg-easy \
  -e LANG=en \
  -e WG_HOST= <public-IP>\
  -e PASSWORD_HASH=<pass> \
  -e PORT=51821 \
  -e WG_PORT=51820 \
  -e WG_DEVICE=enp1s0 \
  -e WEBUI_HOST=<server-IP> \
  -e WG_ALLOWED_IPS=0.0.0.0/0, ::/0, 192.168.1.0/24, 10.8.0.0/24, 172.17.0.0/16 \
  -v ~/.wg-easy:/etc/wireguard \
  --network host \
  --cap-add=NET_ADMIN \
  --cap-add=SYS_MODULE \
  --restart unless-stopped \
  ghcr.io/wg-easy/wg-easy
```

## Environment Variables
`LANG:` Language setting for the application. \
`WG_HOST:` The public hostname or IP address of your WireGuard server. \
`PASSWORD_HASH:` The password hash for accessing the web UI. \
`PORT:` The port for the web UI. \
`WG_PORT:` The WireGuard port. \
`WG_DEVICE:` Network device to use for WireGuard. \
`WEBUI_HOST:` The IP address or hostname where the web UI will be accessible. \
`WG_ALLOWED_IPS:` List of IP ranges allowed to connect to the WireGuard server. \
`-v ~/.wg-easy:/etc/wireguard:` Mounts the ~/.wg-easy directory to /etc/wireguard in the container. 

## wg-password 
`wg-password` (or wgpw) is a script that generates bcrypt password hashes for use with wg-easy, enhancing security by requiring passwords.

**Features** \
Generate bcrypt password hashes. 
Easily integrate with wg-easy to enforce password requirements. 

**Usage with Docker** \
To generate a bcrypt password hash using Docker, run the following command: 
```bash
docker run ghcr.io/wg-easy/wg-easy wgpw YOUR_PASSWORD
```
**Important:** \
Make sure to enclose your password in single quotes when running the Docker command and then replacing each $ symbol with $$: \

Example:
```bash
echo '$2b$12$coPqCsPtcFO.Ab99xylBNOW4.Iu7OOA2/ZIboHN6/oyxca3MWo7fW'
```

## Info 
I strongly recommend to use **CasaOS** for password debuging as sometimes are some errors in reading the **password** 

This repo was created as an addapted and easy remember from original post: **https://github.com/wg-easy/wg-easy**
