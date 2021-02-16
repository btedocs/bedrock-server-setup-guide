# Nederlands

![](.gitbook/assets/serverguide.png)

Deze gids gaat er van uit dat je een functionele Minecraft Forge server met Cubic Chunks draaiende hebt.

Wanneer je configuratie bestanden aan het bewerken bent zorg er dan voor dat je het bestand hebt opgeslagen voordat je verder gaat met de volgende stap!

Voordat je begint: Het is _essentieel_ dat je alle verplichte client-side mods van je server \(behalve Cubic Chunks\) verwijdert, zo kan een speler met niks anders dan Minecraft Forge en Cubic Chunks geïnstalleerd de server kan joinen. Als extra mods verplicht zijn kunnen vanilla spelers niet verbinden met de server.

## Server instellen

1. Download de laatste versie van Cubic Chunks van [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). Je wilt `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Vervang de actuele Cubic Chunks jar in je server's `mods` folder met de zojuist gedownloade, herstart dan je server.
3. Verander `allowVanillaClients` naar `true` in `config/cubicchunks.cfg`.

   ```bash
    # Sta spelers toe om zonder cubic chunks de server te kunnen joinen. DIT IS BEDOELD VOOR DE VANILLA SPELERS. Dit zal ZEER waarschijnlijk breken bij gebruik met andere mods.
    B:allowVanillaClients=true
   ```

4. Als jouw server geen deel van een network is en je wilt geen vanilla spelers ondersteunen op andere versies dan Java Edition 1.12.2, ben je klaar. Herstart de server en geniet! Ga anders verder.
5. Verander `online-mode` naar `false` in `server.properties`.

   ```text
   online-mode=false
   ```

6. Als je server op Mohist draait ga dan door naar [Mohist Setup](nederlands.md#mohist-setup). Ga anders door naar [Forge Setup](nederlands.md#forge-setup).

### Mohist Setup

_Het volgende deel is bedoeld voor servers die Mohist gebruiken! Als je geen Mohist gebruikt kan je skippen naar_ [_Forge Setup_](nederlands.md#forge-setup)_._

1. Download de laatste versie van [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/).
2. Vervang de actuele Mohist jar in je server folder met de zojuist gedownloade. Hernoem die als dat nodig is. 
3. Verander `bungeecord` naar `true` in `spigot.yml`.

   ```text
   bungeecord: true
   ```

4. Herstart de server.
5. Klaar! Je kan door naar [Proxy Setup](nederlands.md#proxy-setup).

### Forge Setup

_Het volgende deel is bedoeld voor servers die **geen** Mohist gebruiken! Als je Mohist gebruikt moet je terug gaan naar_ [_Mohist Setup_](nederlands.md#mohist-setup)_._

Opmerking: de volgende mod is genoodzaakt BungeeCord IP forwarding in te kunnen schakelen op Forge zonder SpongeForge te gebruiken \(SpongeForge is niet beschikbaar op Cubic Chunks\).

1. Download de laatste versie van SpeedBoost van [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Plaats de gedownloade mod in je server's `mods` folder en herstart de server.
3. Vind de `bungeecord` sectie in `config/speedboost_config.json` en verander `state` naar `true`.

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. Herstart de server.
5. Klaar! Je kan door naar [Proxy Setup](nederlands.md#proxy-setup).

## Proxy Setup

_Als je server's Waterfall proxy is gehost door iemand anders \( je hebt bijvoorbeeld een build server die deel van de BuildTheEarth Big Network is draaiende, dan ben je klaar._

Deze gids gaat ervan uit dat je al een Waterfall proxy set up draaiende hebt. Als je al een BungeeCord proxy hebt, kan je simpelweg [de laatste versie downloaden](https://papermc.io/downloads#Waterfall) en vervang de BungeeCord jar. Heb je dit niet, volg de [official setup guide](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) en configureer het om verbinding te maken met je backend Forge server.

### Waterfall Setup

Opmerking: totdat [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) is samengevoegd is er nog geen officiële download bron voor ViaVersion.

1. Verander `forge_support` naar `true` in `config.yml`.

   ```text
   forge_support: true
   ```

2. Verander `ip_forward` naar `true` in `config.yml`.

   ```text
   ip_forward: true
   ```

3. Download het volgende:  

   Geyser van [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)  

   ViaVersion van [here](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Aanbevolen:_ Floodgate van [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Optioneel:_ ViaBackwards van [Jenkins](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Optioneel:_ ViaRewind van [Jenkins](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

4. Plaats alle gedownloade bestanden in Waterfall's `plugins` folder, herstart Waterfall dan.
5. Verander `suppress-conversion-warnings` naar `true` in `plugins/ViaVersion/config.yml`.

   ```text
   # We waarschuwen wanneer er een error is die items en blok-data omzet over versies. Moeten wij deze onderdrukken? (Alleen gesuggereerd bij spam).
   suppress-conversion-warnings: true
   ```

6. Verander `general-thread-pool` naar het aantal kernen op je  Waterfall server in `plugins/Geyser-BungeeCord/config.yml`. Bij 8 kernen bijvoorbeeld:

   ```text
   # Thread pool size
   general-thread-pool: 8
   ```

7. Verander `cache-chunks` naar `true` in `plugins/Geyser-BungeeCord/config.yml`. Negeer de waarschuwingen, want dit deel is essentieel om Bedrock te laten functioneren met Cubic Chunks.

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

8. _Als je Floodgate hebt gedownload:_ Vind de `player-link` sectie in `plugins/floodgate-bungee/config.yml` en verander `enable` naar `true`.

   ```text
   # Authenticatie type. Kan offline, online of floodgate(zie https://github.com/GeyserMC/Geyser/wiki/Floodgate).
   auth-type: floodgate
   ```

9. _Als je Floodgate hebt gedownload:_ Vind de `remote` sectie in `plugins/Geyser-BungeeCord/config.yml` en verander `auth-type` naar `floodgate`.

   ```text
   # Of het koppelingssysteem moet worden ingeschakeld. Als u dit uitschakelt voorkomt dit dat
   # spelers de koppelingsfunctie gebruiken, zelfs als ze al zijn gekoppeld.
   enable: true
   ```

10. Herstart Waterfall.

Gefeliciteert! Je kan nu verbinden met je Cubic Chunks server via Waterfall met de volgende versies:

* Cubic Chunks 1.12.2
* Vanilla Java Edition 1.12.2-1.16.3
* Bedrock Edition
* _Als je ViaBackwards hebt gedownload:_ Vanilla Java Edition 1.9-1.16.3
* _Als je ViaRewind hebt gedownload:_ Vanilla Java Edition 1.7-1.16.3

## Aanvullende opmerkingen:

### ViaRewind en BungeeTabListPlus

Als je ViaRewind in combinatie met BungeeTabListPlus op Waterfall gebruikt, creeër een nieuw bestand `1-7-10.yml` in `plugins/BungeeTabListPlus/tabLists` met de volgende inhoud:

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

Dit is nodig om het breken van \(speler\)skins en namen van spelers die 1.7.10 of lager gebruiken te voorkomen.

