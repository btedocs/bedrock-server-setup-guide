# Español

![](.gitbook/assets/serverguide.png)

Esta guía asume que ya tienes un servidor de Minecraft Forge funcional con Cubic Chunks ajustado y corriendo.

Al editar los archivos de configuración, ¡asegúrate de guardar el archivo antes de proceder al siguiente paso!

Antes de comenzar: es _absolutamente crítico_ que remuevas todos los mods requeridos por el cliente de tu server \(exceptuando Cubic Chunks\) para que un jugador sin nada más que Minecraft Forge y Cubic Chunks se pueda unir al server. Si mods adicionales son requeridos, ¡los jugadores de vanilla no se podrán conectar!

## Preparación del Server

1. Descarga la última versión de Cubic Chunks de [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). Querrás `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Reemplaza el jar de Cubic Chunks actual en `mods` de la carpeta de tu servidor con el recién descargado,  entonces reinicia el servidor.
3. Cambia `allowVanillaClients`a `true`en `config/cubicchunks.cfg`.

   ```bash
    # Allows clients without cubic chunks to join. THIS IS INTENDED FOR VANILLA CLIENTS. This is VERY likely to break when used with other mods     
    B:allowVanillaClients=true
   ```

4. Si tu servidor no es parte de una red y no deseas soportar Clientes Vanilla en versiones distintas a Java 1.12.2, estás listo. ¡Reinicia tu servidor y provecho! De lo contrario, continua.
5. Cambia `online-mode`a `false`en `server.properties`

   ```text
   online-mode=false
   ```

6. Si tu servidor está corriendo Mohist entonces procede a [Preparación De Mohist](espanol.md#preparacion-de-mohist). De otro modo, procede a [Preparación De Forge](espanol.md#preparacion-de-forge).

### Preparación de Mohist

_¡La siguiente sección solo está dirigida a dueños de server usando Mohist! Si no estás usando Mohist, puedes saltar hasta_ [_Preparación de Forge_](espanol.md#preparacion-de-forge)

1. Descarga la última versión de Mohist de [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/).
2. Reemplaza el jar del Mohist actual en la carpeta del servidor con el recién descargado, renombrando el nuevo si es necesario.
3. Cambia `bungeecord`a `true`en `spigot.yml`

   ```text
   bungeecord: true
   ```

4. Reinicia tu servidor.
5. ¡Hecho! Puedes ir a [Preparación Del Proxy](espanol.md#preparacion-del-proxy).

### Preparación de Forge

_¡La siguiente sección está dirigida solo para dueños de servidores **no** usan Mohist! Si no estás usando Mohist, puedes volver a_ [_Preparación de Mohist_](espanol.md#preparacion-de-mohist)_._

Nota: el siguiente mod es requerido para activar el Reenvío de IP de BungeeCord en Forge sin SpongeForge \(ya que SpongeForge es incompatible con Cubic Chunks\).

1. Descarga la última versión de SpeedBoost de [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Pone el mod recién descargado en la carpeta de los `mods` de tu server y reinícialo. 
3. Encuentra la sección de `bungeecord` en `config/speedboost_config.json` y cambia `state`a `true`.

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. Reinicia tu servidor.
5. ¡Hecho! Ahora puedes proceder a [Preparación del Proxy](espanol.md#preparacion-del-proxy)

## **Preparación del Proxy**

_Si el proxy de Cascada\(Waterfall\) de tu servidor está hosteado por alguien más \(por ejemplo, si estás ejecutando un server como parte de la Gran Red De BuildTheEarth\), entonces ya estás listo._

Esta guía asume que ya tienes un proxy de Cascada \(Waterfall\) listo y en funcionamiento. Si ya tienes un proxy de BungeeCord, puedes simplemente [descargar la última versión de Waterfall](https://papermc.io/downloads#Waterfall) y reemplazar el jar de BungeeCord. O si no, sigue la [guía oficial de preparación](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) y configúralo para que se conecte al servidor backend de Forge .

### Preparación de Waterfall

Nota: hasta que [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) se fusionen, no hay una fuente de descarga oficial para ViaVersion.

1. Cambia `forge_support`a `true`en `config.yml`.

   ```text
   forge_support: true
   ```

2. Cambia `ip_forward`a `true`en `config.yml`.

```text
ip_forward: true
```

1. Descarga lo siguiente: Geyser de [Jenkins](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar) 

   ViaVersion desde [acá](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Recomendado:_ Floodgate desde [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Opcional:_ ViaBackwards desde [Jenkins](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Opcional:_ ViaRewind desde [Jenkins](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

2. Pone todos los archivos descargados en la carpeta de los `plugins`de Waterfall, y reinicia Waterfall.
3. Cambia `suppress-conversion-warnings`a `true`en `plugins/ViaVersion/config.yml`.

   ```text
   # We warn when there's a error converting item and block data over versions, should we suppress these? (Only suggested if spamming)
   suppress-conversion-warnings: true
   ```

4. Cambia `general-thread-pool`al número de núcleos en tu Servidor de Waterfall en `plugins/Geyser-BungeeCord/config.yml`. Por ejemplo para 8 núcleos:

   ```text
   # Thread pool size
   general-thread-pool: 8
   ```

5. Cambia `cache-chunks`a `true`en `plugins/Geyser-BungeeCord/config.yml`. Ignora las advertencias, porque esta característica es crítica para hacer que los clientes de Bedrock trabajen correctamente con Cubic Chunks.

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

6. _Si descargaste Floodgate:_ Encuentra la sección de `player-link`en `plugins/floodgate-bungee/config.yml`y cambia `enable`a `true`.

   ```text
   # Authentication type. Can be offline, online, or floodgate (see https://github.com/GeyserMC/Geyser/wiki/Floodgate).
   auth-type: floodgate
   ```

7. _Si descargaste FloodGate:_ Encuentra la sección `remote` en `plugins/Geyser-BungeeCord/config.yml` y cambia `auth-type` a `floodgate`. 

   ```text
   # Whether to enable the linking system. Turning this off will prevent
   # players from using the linking feature even if they are already linked.  
   enable: true
   ```

8. Reinicia Waterfall.

¡Felicitaciones! Ahora te puedes conectar al Servidor de Cubic Chunks a través de Waterfall con cualquiera de los siguientes clientes:

* Cubic Chunks 1.12.2
* Vanilla Java Edition 1.12.2-1.16.3
* Bedrock Edition
* _Si descargaste ViaBackwards:_ Vanilla Java Edition 1.9-1.16.3
* _Si descargaste ViaRewind:_ Vanilla Java Edition 1.7-1.16.3

## Notas adicionales:

### ViaRewind y BungeeTabListPlus

Si estás usando ViaRewind en combinación con BungeeTabListPlust en Waterfall, crea un nuevo archivo `1-7-10.yml`en `plugins/BungeeTablListPlus/tabLists`con los siguientes contenidos:

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

Esto es requerido para evitar jugadores rompiendo skins y name tags para jugadores corriendo 1.7.10 para abajo.

