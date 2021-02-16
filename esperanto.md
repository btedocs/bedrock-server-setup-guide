# Esperanto

![](.gitbook/assets/serverguide.png)

Ĉi tiu gvido akceptas ke vi jam havas funkciantan Minecraft-Forge-Servilon kun aktiva kaj funkcianta Cubic Chunks.

Dum la redaktado de la agordaj dosieroj, certiĝu konservi la dosieron antaŭ la procedo de la sekvanta paŝo!

Antaŭ vi komenciĝas: ĝi estas _nepre kriza_ ke vi forigas ĉiujn klientflankajn necesajn modifojn el via servilo \(ekster Cubic Chunks\) por ke ludanto kun nenion escepte de instalitaj Minecraft Forge kaj Cubic Chunks povas aligi al servilo. Se kromaj modifoj necesas, vanilla-ludantoj ne povos konekti!

## Servila Aranĝo

1. Elŝutu la lastan Cubic Chunks version el [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). Vi volas `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Anstataŭigu la aktualan jar Cubic Chunks en via servila dosierujon `mods` kun la ĵus elŝutita, kaj restartigu la servilon.
3. Ŝanĝigu `allowVanillaClients` al `true` en `config/cubicchunks.cfg`.

   ```bash
    # Ĝi permesas aligi al klientoj sen Cubic Chunks. ĈI TIO INTENCAS POR VANILLA KLIENTOJ. Ĉi tio TRE verŝajne rompigos kiam uzita kun aliaj modifoj

    B:allowVanillaClients=true
   ```

4. Se via servilo ne estas parto de reto kaj vi ne deziras subteni escepte de Java Edition 1.12.2, vi estas kompleta. Restartigu vian servilon kaj ĝuu! Alimaniere, kontinuu. 
5. Ŝanĝigu `online-mode` al `false` en `server.properties`.

   ```text
   online-mode=false
   ```

6. Se via servilo lanĉas Mohist kaj poste iru al [Mohist Aranĝo](esperanto.md#mohist-aran-o). Alimaniere, progresu al [Forge Aranĝo](esperanto.md#forge-aran-o).

### Mohist Aranĝo

_La sekvanta sekcio intencas nur por servilaj posedantoj uzante Mohist! Se vi ne uzas Mohist, vi povas preterpasi al_ [_Forge Aranĝo_](esperanto.md#forge-aran-o)_._

1. Elŝutu la lastan version de Mohist el [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/). 
2. Anstataŭigu la aktualan Jar-Mohist en via servila dosiero kun la ĵus elŝutita, renomante la novaĵo se ĝi necesas. 
3. Ŝanĝigu `bungeecord` al `true` en `spigot.yml`. 

   ```text
   bungeecord: true
   ```

4. Restartigu la servilon.
5. Fata! Vi povas progresi al [Prokura Aranĝo](esperanto.md#prokura-aran-o).

### Forge Aranĝo

_La sekvanta sekcio intencas nur por la servilaj posedantoj **ne** uzante Mohist! Se vi uzas Mohist, vi devus reiri al_ [_Mohist Aranĝo_](esperanto.md#mohist-aran-o)_._

Noto: la sekvanta modifo necesas ŝaltado de IP-plusendado BungeeCord en Forge sen SpongeForge \(ĉar SpongeForge ne kongruas kun Cubic Chunks\).

1. Elŝutu la lastan version de SpeedBoost el [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Metu la ĵus elŝutitan modigon en via servila dosierujo `mods` kaj restartigu la servilon.
3. Trovu la `bungeecord` sekcion en `config/speedboost_config.json` kaj ŝanĝigu `state` al `true`.

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. Restartigu vian servilon.
5. Fata! Vi povas progresi al [Proxy Agordo](esperanto.md#prokura-aran-o).

## Prokura Aranĝo

_Se la servila proxy Waterfall estas gastiganta de aliulo \(ekzemple, vi lanĉas konstruan servilon kiel parton de la BuildTheEarth Big Network\), tiam vi estas preta._

Ĉi tiu gvido supozas ke via prokura Waterfall jam staras kaj funkcias. Se vi jam havas prokuran BungeeCord, vi povas simple [elŝutu la lastan version de Waterfall](https://papermc.io/downloads#Waterfall) kaj anstataŭigu la jar BungeeCord. Se ne, agu laŭ la [oficiala agorda gvido](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) kaj agordu ĝin por ke ĝi konektu al via interna servilo Forge.

### Waterfall Aranĝo

Noto: ĝis [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) unuigas, ne estas oficiala elŝutejo por ViaVersion.

1. Ŝanĝigu `forge_support` al `true` en `config.yml`.

   ```text
   forge_support: true
   ```

2. Ŝanĝigu `ip_forward` al`true` en `config.yml`.

   ```text
   ip_forward: true
   ```

3. Elŝutu la jenon:  

   Geyser el [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)  

   ViaVersion el [ĉi tie](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Rekomenditaj:_ Floodgate el [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Nedeviga:_ ViaBackwards el [Jenkins](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Nedeviga:_ ViaRewind el [Jenkins](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

4. Metu ĉiujn elŝutitajn dosierojn en la dosierujo Waterfall `plugins`, kaj poste restartigu Waterfall.
5. Ŝanĝigu `suppress-conversion-warnings` al `true` en `plugins/ViaVersion/config.yml`.

   ```text
   # Ni avertas kiam estas eraro en la konverto de ero kaj bloka datumo pasinta la versioj, ĉu ni devus forigi ĉi tiujn? (Nur sugesti en spamado) 
   suppress-conversion-warnings: true
   ```

6. Ŝanĝigu `general-thread-pool` al nombro de kernoj en via servilo Waterfall en `plugins/Geyser-BungeeCord/config.yml`. Ekzemple por 8 kernoj:

   ```text
   # Fadena grandeco
   general-thread-pool: 8
   ```

7. Ŝanĝigu `cache-chunks` al `true` en`plugins/Geyser-BungeeCord/config.yml`. Ignorante la avertojn estas kriza por ke klientoj Bedrock funkcias ĝuste kun Cubic Chunks.

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

8. _Se vi elŝutis Floodgate:_ Trovu la sekcion `player link` en `plugins/floodgate-bungee/config.yml` kaj ŝanĝigu `enable` al `true`.

```text
  # Aŭtentigotipo. Ĝi povas esti offline, online aŭ floodgate (vidu https://github.com/GeyserMC/Geyser/wiki/Floodgate).
  auth-type: floodgate
```

1. _Se vi elŝutis Floodgate:_ Trovu la sekcion `remote` en `plugins/Geyser-BungeeCord/config.yml` kaj ŝanĝigu `auth-type` al`floodgate`.

   ```text
   # Ĉu ebligi la kunliga sistemo. Elŝatado de ĉi tio malhelpas
   # ludantojn por uzi la kunligeblon eĉ se ili jam estas kunligitaj.
   enable: true
   ```

2. Restartigu Waterfall.

Gratulojn! Vi povas nun konekti al via servilo Cubic Chunks tra Waterfall kun ajna el la jenaj klientoj:

* Cubic Chunks 1.12.2
* Vanilla Java Edition 1.12.2-1.16.3
* Bedrock Edition
* _Se vi elŝutis ViaBackwards:_ Vanilla Java Edition 1.9-1.16.3
* _Se vi elŝutis ViaRewind:_ Vanilla Java Edition 1.7-1.16.3

## Kromaj notoj:

### ViaRewind kaj BungeeTabListPlus

Se vi uzas ViaRewind kune kun BungeeTabListPlus en Waterfall, kreu novan dosieron `1-7-10.yml` kun la jenaj enhavoj:

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

Ĉi tio necesas por malhelpi la rompo de ludantaj haŭtoj kaj nomŝildoj de ludantoj lanĉante 1.7.10 kaj suben.

