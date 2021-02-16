# English

![](.gitbook/assets/serverguide.png)

This guide assumes you already have a functional Minecraft Forge server with Cubic Chunks set up and running.

When editing configuration files, make sure to save the file before proceeding to the next step!

Before you begin: it is _absolutely critical_ that you remove all client-side required mods from your server \(aside from Cubic Chunks\) so that a player with nothing other than Minecraft Forge and Cubic Chunks installed can join the server. If additional mods are required, vanilla players will not be able to connect!

## Server Setup

1. Download the latest version of Cubic Chunks from [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). You want `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Replace the current Cubic Chunks jar in your server's `mods` folder with the newly downloaded one, then restart the server.
3. Change `allowVanillaClients` to `true` in `config/cubicchunks.cfg`.

   ```bash
    # Allows clients without cubic chunks to join. THIS IS INTENDED FOR VANILLA CLIENTS. This is VERY likely to break when used with other mods
    B:allowVanillaClients=true
   ```

4. If your server is not part of a network and you do not wish to support vanilla clients on versions other than Java Edition 1.12.2, you are now complete. Restart your server and enjoy! Otherwise, continue.
5. Change `online-mode` to `false` in `server.properties`.

   ```text
   online-mode=false
   ```

6. If your server is running Mohist then proceed to [Mohist Setup](./#mohist-setup). Otherwise, proceed to [Forge Setup](./#forge-setup).

### Mohist Setup

_The following section is intended only for server owners using Mohist! If you're not using Mohist, you can skip to_ [_Forge Setup_](./#forge-setup)_._

1. Download the latest version of Mohist from [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/).
2. Replace the current Mohist jar in your server folder with the newly downloaded one, renaming the new one if necessary.
3. Change `bungeecord` to `true` in `spigot.yml`.

   ```text
   bungeecord: true
   ```

4. Restart your server.
5. Done! You can proceed to [Proxy Setup](./#proxy-setup).

### Forge Setup

_The following section is intended only for server owners **not** using Mohist! If you're using Mohist, you should return to_ [_Mohist Setup_](./#mohist-setup)_._

Note: the following mod is required to enable BungeeCord IP forwarding on Forge without SpongeForge \(as SpongeForge is incompatible with Cubic Chunks\).

1. Download the latest version of SpeedBoost from [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Place the newly downloaded mod in your server's `mods` folder and restart the server.
3. Find the `bungeecord` section in `config/speedboost_config.json` and change `state` to `true`.

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. Restart your server.
5. Done! You can proceed to [Proxy Setup](./#proxy-setup).

## Proxy Setup

_If your server's Waterfall proxy is hosted by someone else \(for example, you are running a build server as part of the BuildTheEarth Big Network\), then you are done._

This guide assumes you already have a Waterfall proxy set up and running. If you already have a BungeeCord proxy, you can simply [download the latest version of Waterfall](https://papermc.io/downloads#Waterfall) and replace the BungeeCord jar. If not, follow the [official setup guide](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) and configure it to connect to your backend Forge server.

### Waterfall Setup

Note: until [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) is merged, there is no official download source for ViaVersion.

1. Change `forge_support` to `true` in `config.yml`.

   ```text
   forge_support: true
   ```

2. Change `ip_forward` to `true` in `config.yml`.

   ```text
   ip_forward: true
   ```

3. Download the following:  

   Geyser from [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)  

   ViaVersion from [here](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Recommended:_ Floodgate from [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Optional:_ ViaBackwards from [Jenkins](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Optional:_ ViaRewind from [Jenkins](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

4. Place all of the downloaded files into Waterfall's `plugins` folder, then restart Waterfall.
5. Change `suppress-conversion-warnings` to `true` in `plugins/ViaVersion/config.yml`.

   ```text
   # We warn when there's a error converting item and block data over versions, should we suppress these? (Only suggested if spamming)
   suppress-conversion-warnings: true
   ```

6. Change `general-thread-pool` to the number of cores on your Waterfall server in `plugins/Geyser-BungeeCord/config.yml`. Example for 8 cores:

   ```text
   # Thread pool size
   general-thread-pool: 8
   ```

7. Change `cache-chunks` to `true` in `plugins/Geyser-BungeeCord/config.yml`. Disregard the warnings, because this feature is critical to making Bedrock clients work correctly with Cubic Chunks.

   ```text
   # Configures if chunk caching should be enabled or not. This keeps an individual
   # record of each block the client loads in. While this feature does allow for a few
   # things such as block break animations to show up in creative mode and among others,
   # it is HIGHLY recommended you disable this on a production environment as it can eat
   # up a lot of RAM. However, when using the Spigot version of Geyser, support for features
   # or implementations this allows is automatically enabled without the additional caching as
   # Geyser has direct access to the server itself.
   cache-chunks: true
   ```

8. _If you downloaded Floodgate:_ Find the `player-link` section in `plugins/floodgate-bungee/config.yml` and change `enable` to `true`.

   ```text
   # Authentication type. Can be offline, online, or floodgate (see https://github.com/GeyserMC/Geyser/wiki/Floodgate).
   auth-type: floodgate
   ```

9. _If you downloaded Floodgate:_ Find the `remote` section in `plugins/Geyser-BungeeCord/config.yml` and change `auth-type` to `floodgate`.

   ```text
   # Whether to enable the linking system. Turning this off will prevent
   # players from using the linking feature even if they are already linked.
   enable: true
   ```

10. Restart Waterfall.

Congratulations! You can now connect to your Cubic Chunks server through Waterfall with any one of the following clients:

* Cubic Chunks 1.12.2
* Vanilla Java Edition 1.12.2-1.16.3
* Bedrock Edition
* _If you downloaded ViaBackwards:_ Vanilla Java Edition 1.9-1.16.3
* _If you downloaded ViaRewind:_ Vanilla Java Edition 1.7-1.16.3

## Additional notes:

### ViaRewind and BungeeTabListPlus

If you are using ViaRewind in combination with BungeeTabListPlus on Waterfall, create a new file `1-7-10.yml` in `plugins/BungeeTabListPlus/tabLists` with the following contents:

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

This is required to avoid breaking player skins and name tags for players running 1.7.10 and below.

