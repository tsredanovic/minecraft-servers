# Minecraft Servers

My personal set up and instructions for running Minecraft servers.


## First time set up instructions

1. Clone this repository

2. Create an empty `worlds` directory inside the root `minecraft-server` directory


## World set up instructions

1. Create an empty directory for your world inside the `worlds` directory and name it whatever you want (example: `world1`)

2. Create a `compose.yaml` file in the `world1` with contents of the `compose.yaml.example` file and adjust it with desired settings for your world
   - `minecraft-server` service:
     - Change `MOTD` to the display name of your world
     - Change `DIFFICULTY`, `WHITELIST` and `OPS` to the desired settings
     - Change `volumes` to the desired paths (left side) for your world data and mods (example: `./data` and `./mods`)
     - Change `RCON_PASSWORD` to something strong
     - Change `MEMORY` to the desired amount of memory
     - Change host ports (left sided) to desired ports for you minecraft server
     - (Optional) Change the `ICON` to the icon you want to use for your world - you can use the links provided in `Icons` section or your own
   - `minecraft-server-backup` service:
     - Change `RCON_PASSWORD` to match values in the `minecraft-server` service
     - Change `volumes` to the desired paths (left side) for your world data and backups (example: `./data` and `./backups`)
     - (Optional) Change `BACKUP_INTERVAL` and `PRUNE_BACKUPS_DAYS` to desired values, for more options see [mc-backup](https://github.com/itzg/mc-backup)

3. (Optional) Set up mods
   - Create an empty `mods` directory inside your `world1` directory
   - Place your mods inside the `mods` directory - some useful mods are listed in `Mods` section

4. Run `docker compose up -d` inside the `world1` directory to start your server
   - (Optional) Run `docker compose logs -f` to follow the logs
   - This is enough for LAN gameplay, if you want to share your server online, you will need to set up port forwarding

5. (Optional) Set up port forwarding
   - Find port forwarding settings for your router
   - Set up port forwarding for your minecraft server port (25565)
   - Your server should be reachable at `{your_public_ip}:25565`, if you want to replace your public IP with a domain, you will need to set up DNS records

6. (Optional) Set up DNS records on CloudFlare
   - Open your CloudFlare dashboard and select your domain
   - Go to `DNS` tab, click `Add record`
     - Fill in with following values:
       - Type: A
       - Name: world1
       - IPv4 address: {your_public_ip}
       - Proxy status: DNS only
   - Go to `DNS` tab, click `Add record`
     - Fill in with following values:
       - Type: SRV
       - Name: _minecraft._tcp.world1
       - Priority: 0
       - Weight: 0
       - Port: 25565
       - Target: world1.{your_domain}
   - Your server should be reachable at `world1.{your_domain}`, if you have a dynamic IP you will need to automatically update DNS records to keep it pointing to your server

7. (Optional) Automatically update A records on CloudFlare
   - Follow the instructions in [DynamicFlare](https://github.com/tsredanovic/dynamicflare)


## Mods

### Fabric

#### Lithium (Fabric)

https://www.curseforge.com/minecraft/mc-mods/lithium

- general-purpose optimization
- works on both the client and server, and can be installed on servers without requiring clients to also have the mod

#### Phosphor (Fabric) - DEPRECATED

https://www.curseforge.com/minecraft/mc-mods/phosphor

- lighting engine optimization
- works on both the client and server, and can be installed on servers without requiring clients to also have the mod
- incompatible with `Starlight (Fabric)`
- use `Moonrise (Fabric)` instead

#### Starlight (Fabric) - DEPRECATED

https://www.curseforge.com/minecraft/mc-mods/starlight

- lighting engine optimization
- works on both the client and server, and can be installed on servers without requiring clients to also have the mod
- incompatible with `Phosphor (Fabric)`
- use `Moonrise (Fabric)` instead

#### Moonrise (Fabric)

https://www.curseforge.com/minecraft/mc-mods/moonrise

- official port of several important Paper patches
- works on both the client and server, and can be installed on servers without requiring clients to also have the mod


## Icons

### Forest Fox

https://i.ibb.co/zJFc8vV/forest-fox.png

![](https://i.ibb.co/zJFc8vV/forest-fox.png)

### Forest Ruins

https://i.ibb.co/JkNDKCW/forest-ruins.png

![](https://i.ibb.co/JkNDKCW/forest-ruins.png)

### Kingdom Overlook

https://i.ibb.co/HdY0L9z/kingdom-overlook.png

![](https://i.ibb.co/HdY0L9z/kingdom-overlook.png)

### Mountain Scene

https://i.ibb.co/JtW5H0C/mountain-scene.png

![](https://i.ibb.co/JtW5H0C/mountain-scene.png)

### Mountain Side Lake

https://i.ibb.co/1ssNJNK/mountain-side-lake.png

![](https://i.ibb.co/1ssNJNK/mountain-side-lake.png)

### Thorny Jungle Heart

https://i.ibb.co/w6S1YzD/thorny-jungle-heart.png

![](https://i.ibb.co/w6S1YzD/thorny-jungle-heart.png)

### Zen Land

https://i.ibb.co/SQHXX95/zen-land.png

![](https://i.ibb.co/SQHXX95/zen-land.png)
