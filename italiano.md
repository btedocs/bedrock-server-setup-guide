# Italiano

![](.gitbook/assets/serverguide.png)

Questa guida presume che già abbia un server operativo de Minecraft Forge con Cubic Chunks allestito e funzionante.

Quando modifica gli files de configurazione, fa sicuro che guardi il file prima di procedere al prossimo passo!

Prima di cominciare: è _assolutamente essenziale_ che rimuovi tutti mods del lato cliente del tuo server \(a parte de Cubic Chunks\) in modo che un giocatore senza niente più che Minecraft Forge e Cubic Chunks installati possano unirsi al server. Se ulteriori mods sono richiesti, giocatori de vanilla non potranno unirsi!

## Setup Del Server

1. Scarica la ultima versione de Cubic Chunks da [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). Vuoi `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Sostituisca la attuala Cubic Chunks jar in la cartella `mods` del tuo server con la appena scaricata, poi inizia di nuovo il server.
3. Cambia `allowVanillaClients` al `true` in `config/cubicchunks.cfg`.

   ```bash
    # Lascia che clients senza cubic chunks si uniscano. Questo è molto probabile che si rompa quando è usato con altri mods  
    B:allowVanillaClients=true
   ```

4. Se il tuo server non è parte de un network e non vuoi supportare vanilla clients in versioni a parte de Java Edition 1.12.2, sei pronto. Inizia di nuovo il tuo server e diverta! Altrimenti, continua.
5. Cambia `online-mode` al `false` in `server.properties`.

   ```text
   online-mode=false
   ```

6. Se il tuo server fa andare Mohist, allora vada a [Setup de Mohist](italiano.md#setup-de-mohist). Altrimenti, vada a [Setup De Forge](italiano.md#setup-de-forge).

### Setup de Mohist

_La seguente parte è destinata solo per gli proprietari di servers chi usano Mohist! Se non usi Mohist, puoi saltare a_ [_Setup De Forge_](italiano.md#setup-de-forge)_._

1. Scarica la ultima versione de Mohist da [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/).
2. Sostituisca la attuala Mohist jar in la cartella del tuo server con la appena scaricata, rinominando la nuova se è necessario.
3. Cambia `bungeecord` al `true` in `spigot.yml`.

```text
  bungeecord: true
```

1. Inizia il tuo server di nuovo.
2. Fatto! Puoi avanzare a [Setup Del Proxy](italiano.md#setup-del-proxy).

### Setup De Forge

_La parte seguente è destinata solo per proprietari di servers chi **non** usano Mohist! Se non si utilizza Mohist, dovresti ritornare a_ [_Mohist Setup_](italiano.md#setup-de-mohist)_._

Nota: il seguente mod è richiesto per attivare BungeeCord IP Forwarding in Forge senza SpongeForge \(siccome SpongeForge è incompatibile con Cubic Chunks\).

1. Scarica la ultima versione de SpeedBoost da [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Metta il mod appena scaricato in la cartella `mods` del tuo server e inizia il server di nuovo.
3. Trova la parte `bungeecord` in `config/speedboost_config.json` e cambia `state` al `true`.

```javascript
  "bungeecord": {
    "state": true
  },
```

1. Inizia il server di nuovo.
2. Fatto! Puoi andare a [Setup Del Proxy](italiano.md#setup-del-proxy).

## Setup Del Proxy

_Se il proxy Waterfall del tuo server è ospitato da qualcun'altro \(per esempio, tu fai andare un server de costruzione come parte de la BuildTheEarth Big Network\), sei pronto_

Questa guida presume che tu già abbia un proxy Waterfall allestito e funzionante. Se già hai un proxy de Bungeecord, puoi semplicemente [scaricare la ultima versione de Waterfall](https://papermc.io/downloads#Waterfall) e sostituisca la BungeeCord jar. Se no, segua la [ufficiala guida de setup](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) e configuralo per connettersi al server backend de Forge.

### Setup de Waterfall

Nota: fino a che [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) sia fusi, non c'è una fonte ufficiale de scarico per ViaVersion.

1. Cambia`forge_support` al `true` in `config.yml`.

   ```text
   forge_support: true
   ```

2. Cambia `ip_forward` al `true` in `config.yml`.

   ```text
   ip_forward: true
   ```

3. Scarica lo seguente:  

   Geyser da [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)  

   ViaVersion da [qui](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Raccomandato:_ Floodgate da [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Opzionale:_ ViaBackwards da [Jenkins](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Opzionale:_ ViaRewind da [Jenkins](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

4. Metti tutti file scaricatati nella cartella de `plugins` Waterfall, e puoi inizia Waterfall di nuovo.
5. Cambia `suppress-conversion-warnings` al `true` in `plugins/ViaVersion/config.yml`.

   \`\`\`yml

   **Avvertiamo quando c'è un errore nella conversione de item e dati de blocco tra gli versioni, doviamo sopprimerli? \(Solo suggerito in situazioni de spam\)**

   suppress-conversion-warnings: true

```text
6. Cambia `general-thread-pool` al numero de nuclei nel tuo server in `plugins/Geyser-BungeeCord/config.yml`. Per esempio per otto nuclei:
```yml
# Thread pool size
general-thread-pool: 8
```

1. Cambia`cache-chunks` al `true` in `plugins/Geyser-BungeeCord/config.yml`.  Ignora l'avvertenti, perché questa caratteristica è essenziale per fare che Bedrock Clients funzionino correttamente con Cubic Chunks.

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

1. _Se hai scaricato Floodgate:_ Trova la parte `player-link` in `plugins/floodgate-bungee/config.yml`  e cambia `enable` al `true`.

```text
  # Authentication type. Can be offline, online, or floodgate (see https://github.com/GeyserMC/Geyser/wiki/Floodgate).
  auth-type: floodgate
```

1. _Se hai scaricato Floodgate:_ Trova la parte `remote` in `plugins/Geyser-BungeeCord/config.yml` e cambia `auth-type` al `floodgate`.

   ```text
   # Se attivare il sistema de collegamento o no. Disattivando questo preverrà che
   # giocatori usino la caratteristica de nesso anche se già siano collegato. 
   enable: true
   ```

2. Inizia Waterfall di nuovo.

Congratulazione! Puoi ora connetterti al tuo server de Cubic Chunks per via di Waterfall con uno qualunque degli seguenti clients:

* Cubic Chunks 1.12.2
* Vanilla Java Edition 1.12.2-1.16.3
* Bedrock Edition
* _Se hai scaricato ViaBackwards:_ Vanilla Java Edition 1.9-1.16.3
* _Se hai scaricato ViaRewind:_ Vanilla Java Edition 1.7-1.16.3

## Ulteriore note:

### ViaRewind e BungeeTabListPlus

Se usi ViaRewind in combinazione con BungeeTabListPlus in Waterfall, crea un nuovo file `1-7-10.yml` in `plugins/BungeeTabListPlus/tabLists` con gli seguenti contenuti:

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

Questo è richiesto por prevenire che skins de giocatori e nomi si rompano por giocatori chi fanno andare 1.7.10 e sotto.

