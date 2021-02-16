# Hrvatski

![](.gitbook/assets/serverguide.png)

Ovaj priručnik pretopostavlja da već imate funkcionalan Minecraft Forge server sa Cubic Chunksom.

Prilikom uređivanja konfiguracijskih datoteka, spremite datoteku prije nego što nastavite!

Prije nego što počnete: _apsolutno je kritično_ da s vašeg servera maknete sve modove sa strane klijenta \(osim Cubic Chunksa\) tako da se igrač koji nema ništa osim Minecraft Forgea i Cubic Chunksa može pridružiti serveru. Ako su potrebni dodatni modovi, vanilla igrači se neće moći spojiti!

## Postavljanje Servera

1. Preuzmite najnoviju verziju Cubic Chunksa sa [Jenkinsa](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). Treba vam `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Zamijenite već postojeći Cubic Chunks jar u mapi `mods` vašeg servera s novopreuzetim, zatim ponovno pokrenite server.
3. Promijenite `allowVanillaClients` u `true` u datoteci `config/cubicchunks.cfg`.

   ```bash
    # Allows clients without cubic chunks to join. THIS IS INTENDED FOR VANILLA CLIENTS. This is VERY likely to break when used with other mods
    B:allowVanillaClients=true
   ```

4. Ako vaš server nije dio mreže i ne želite podržavati vanilla klijente na svim verzijama osim Java Edition 1.12.2, gotovi ste. Ponovno pokrenite vaš server i uživajte! Inače, nastavite.
5. Promijenite `online-mode` u `false` u datoteci `server.properties`.

   ```text
   online-mode=false
   ```

6. Ako vaš server koristi Mohist odite do [Postavljanje Mohista](hrvatski.md#postavaljanje-mohista). Inače, odite do [Postavljanje Forgea](hrvatski.md#postavljanje-forgea).

### Postavaljanje Mohista

_Sljedeći dio namijenjen je samo za servere koji koriste Mohist! Ako ne koristite Mohist, odite do_ [_Postavljanje Forgea_](hrvatski.md#postavljanje-forgea)_._

1. Preuzmite najnoviju verziju Mohista sa [Jenkinsa](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/).
2. Zamijenite trenutni Mohist jar u mapi vašeg servera s novopreuzetim, a ako je potrebno, promijenite mu ime.
3. Promijenite `bungeecord` u `true` u datoteci `spigot.yml`.

   ```text
   bungeecord: true
   ```

4. Ponovno pokrenite server.
5. Gotovo! Možete nastaviti do [Postavaljanja Proxyja](hrvatski.md#postavljanje-proxyja).

### Postavljanje Forgea

_Sljedeći dio namijenjen je samo za servere koji **ne** koriste Mohist! Ako koristite Mohist, vratite se na_ [_Postavljanje Mohista_](hrvatski.md#postavaljanje-mohista)_._

Napomena: potreban je sljedeći mod kako bi ste omogućili IP forwarding putem BungeeCorda na Forgeu bez SpongeForgea \(pošto SpongeForge nije kompatibilan sa Cubic Chunksom\).

1. Preuzmite najnoviju verziju SpeedBoosta sa [Jenkinsa](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Stavite novopreuzeti mod u mapu `mods` vašeg servera i ponovno ga pokrenite.
3. Nađite `bungeecord` dio u datoteci `config/speedboost_config.json` i promijenite `state` u `true`.

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. Ponovno pokrenite server.
5. Gotovo! Možete nastaviti do [Postavljanje Proxyja](hrvatski.md#postavljanje-proxyja).

## Postavljanje Proxyja

_Ako Waterfall proxy vašeg servera hosta netko drugi \(primjerice, ako je vaš server u sklopu BuildTheEarth Big Networka\), onda ste gotovi._

Ovaj priručnik pretpostavlja da već imate Waterfall proxy. Ako već imate BungeeCord proxy, možete jednostavno [preuzeti najnoviju verziju Waterfalla](https://papermc.io/downloads#Waterfall) i zamijeniti BungeeCord jar. Ako ne, pratite [službeni priručnik za postavljanje](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) i konfigurirajte ga tako da se spaja na vaš backend Forge server.

### Postavljanje Waterfalla

Napomena: prije nego što se [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) spoji, nema službenog izvora za preuzimanje ViaVersiona.

1. Promijenite `forge_support` u `true` u datoteci `config.yml`.

   ```text
   forge_support: true
   ```

2. Promijenite `ip_forward` u `true` u datoteci `config.yml`.

   ```text
   ip_forward: true
   ```

3. Preuzmite sljedeće:  

   Geyser sa [Jenkinsa](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)  

   ViaVersion [ovdje](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Preporučeno:_ Floodgate sa [Jenkinsa](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Opcionalno:_ ViaBackwards sa [Jenkinsa](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Opcionalno:_ ViaRewind sa [Jenkinsa](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

4. Stavite sve preuzete datoteke u Waterfallovu mapu `plugins`, zatim ponovno pokrenite Waterfall.
5. Promijenite `suppress-conversion-warnings` u `true` u datoteci `plugins/ViaVersion/config.yml`.

   ```text
   # We warn when there's a error converting item and block data over versions, should we suppress these? (Only suggested if spamming)
   suppress-conversion-warnings: true
   ```

6. Promijenite `general-thread-pool` u broj jezgri vašeg Waterfall servera u datoteci `plugins/Geyser-BungeeCord/config.yml`. Primjer za 8 jezgri:

   ```text
   # Thread pool size
   general-thread-pool: 8
   ```

7. Promijenite `cache-chunks` u `true` u datoteci `plugins/Geyser-BungeeCord/config.yml`. Ne obazirite se na upozorenja, pošto je ova značajka nužna kako bi Bedrock klijenti mogli ispravno raditi na Cubic Chunksu.

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

8. _Ako ste preuzeli Floodgate:_ Nađite `player-link` dio u datoteci `plugins/floodgate-bungee/config.yml` i promijenite `enable` u `true`.

   ```text
   # Authentication type. Can be offline, online, or floodgate (see https://github.com/GeyserMC/Geyser/wiki/Floodgate).
   auth-type: floodgate
   ```

9. _Ako ste preuzeli Floodgate:_ Nađite `remote` dio u datoteci `plugins/Geyser-BungeeCord/config.yml` i promijenite `auth-type` u `floodgate`.

   ```text
   # Whether to enable the linking system. Turning this off will prevent
   # players from using the linking feature even if they are already linked.
   enable: true
   ```

10. Ponovno pokrenite Waterfall.

Bravo! Sada se možete spojiti na vaš Cubic Chunks server putem Waterfalla s bilo kojim od sljedećih klijenata:

* Cubic Chunks 1.12.2
* Vanilla Java Edition 1.12.2-1.16.3
* Bedrock Edition
* _Ako ste preuzeli ViaBackwards:_ Vanilla Java Edition 1.9-1.16.3
* _Ako ste preuzeli ViaRewind:_ Vanilla Java Edition 1.7-1.16.3

## Dodatne bilješke:

### ViaRewind i BungeeTabListPlus

Ako koristite ViaRewind skupa sa BungeeTabListPlusom na Waterfallu, napravite novu datoteku `1-7-10.yml` u mapi `plugins/BungeeTabListPlus/tabLists` sa sljedećim sadržajem:

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

Ovo je potrebno kako bi se skinovi i imena igrača prikazivali pravilno za igrače koji igraju na verziji 1.7.10 ili manje.

