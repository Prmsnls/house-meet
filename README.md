[![Discord](https://img.shields.io/discord/821338762134290432?label=Discord)](https://discord.com/invite/CD9UXPgxr8)

![WorkAdventure logo](README-LOGO.svg)
![WorkAdventure office image](README-MAP.png)

**Visit the [House](https://house.prmsnls.xyz)**

# WorkAdventure

WorkAdventure is a web-based collaborative workspace presented in the form of a
16-bit video game. In WorkAdventure you can move around your office and talk to your colleagues (using a video-chat system, triggered when you approach someone).

## Setting up a production 
__Setup for v1.12.11__

- Add DNS Entry for the Instance IP to map it to `house.prmsnls.xyz`
- In the intance, open the port 443 (HTTPS), 80(HTTP), 81(Nginx), 9999(WorkAdventure)
(Port 81 and 9999 will be closed after the Setup)

Docker, Docker-Compose, and NGinX Proxy Manager ([Source](https://github.com/bmcgonag/docker_installs))

Change the permissions on the script to make it executable
`chmod +x install-docker.sh`

Run the installer
`./install-docker.sh`

Login to NGinX Proxy Manager by going to ht<span>tp://</span>house.prmsnls.xyz:81 and use the default credentials: <br />
*username: admin<span>@</span>example.com*
*password: changeme*

### Install WorkAdventure

Clone the Repository
`git clone https://github.com/Prmsnls/house-meet.git`

Open the Repository Folder:
`cd house-meet`

In the environment file (.env) modify following fields accordingly:
- DOMAIN
- ACME_MAIL
- SECRET_KEY
- ADMIN_API_TOKEN

Running docker compose file: 
`docker-compose up`

**WorkAdventure should start at port 9999 `(http://house.prmsnls.xyz:9999)`**

### Setup our Reverse Proxy

- Get the list of all docker networks and note the ids for workadventure_default and nginx networks
`docker network list`

- Get the network details for the networks and note the "Gateway IPs"
`docker network inspect <id>`

- Go to the Nginx dashboard on the browser ht<span>tp://</span>house.prmsnls.xyz:81
    - Add a proxy host for `house.prmsnls.xyz` and map it to **Gateway IP** for WorkAdventure on port **9999**
    - Go to SSL and get a certificate for the domain and toggle the **Force SSL**
    - Add a proxy host for `admin.house.prmsnls.xyz` and map it to **Gateway IP** for Niginx on port **81**.
    - Go to SSL and get a certificate for the domain and toggle the **Force SSL** option.

- Close the port 81 and 9999 from the Firewall.
- WorkAdventure is up on https://house.prmsnls.xyz
