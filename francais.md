# Français

![](.gitbook/assets/serverguide.png)

Quand vous changez les fichiers de configuration, vérifiez que vous avez bien sauvegardé les fichiers avant de passer à l'étape suivante !

Avant de commencer \(c'est _très important_\) vous _devez_ retirer tout les mods côté client qui sont nécessaire \(sauf Cubic Chunks \) pour qu'un joueur qui n'as que Minecraft Forge et Cubic Chunks d'installé peut rejoindre le serveur. Si d'autres mods sont nécessaires, les joueurs avec un client vanilla ne pourront pas se connecter !

## Setup serveur

1. Téléchargez la dernière version de Cubic Chunks depuis [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/). Il faut `CubicChunks-<version>-SNAPSHOT-all.jar`.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. Remplacer le .jar Cubic Chunks actuel dans votre dossire `mods` avec celui que vous venez de télécharger, redémarrer le serveur.
3. Changez `allowVanillaClients` en `true` dans `config/cubicchunks.cfg`.

   ```bash
    # Autoriser les clients sans cubic chunks de rejoindre. CELA EST PRÉVU POUR LES CLIENTS VANILLA. C'est TRÈS probable de ne plus fonctionner si d'autres mod(s) sont utilisés.
    B:allowVanillaClients=true
   ```

4. Si votre serveur ne fait pas parti de notre réseau mais vous voulez suporter les clients vanilla sur des versions différentes que 1.12.2, vous êtes maintenant prêt ! Redémarrer votre serveur et c'est prêt ! Autrement, continuez.
5. Changez `online-mode` en `false` dans `server.properties`.

   ```text
   online-mode=false
   ```

6. Si votre serveur utilise Mohist, vous devez procédez à un [Mohist Setup](francais.md#setup-mohist). Si non, passez au [Forge Setup](francais.md#setup-forge).

### Setup Mohist

_La section suivante est seulement prévue pour les serveurs qui utilisent Mohist! Si vous ne l'utilisez pas, vous pouvez passer au_ [_Forge Setup_](francais.md#setup-forge)_._

1. Télécharger la dernière version de Mohist depuis [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/).
2. Remplacez votre version actuelle du Mohist jar dans votre dossier de mod avec le fichier jar que vous venez de télécharger, renomant le nouveau si nécessaire.
3. Changez `bungeecord` en `true` dans `spigot.yml`.

   ```text
   bungeecord: true
   ```

4. Redémarrez votre serveur.
5. C'est finit ! Vous pouvez maintenant suivre au [Proxy Setup](francais.md#setup-proxy).

### Setup Forge

_La section suivante est seulement prévue pour les serveurs qui **n'utilisent pas** Mohist ! Si vous utilisez Mohist, retournez à lsection pour le_ [_Mohist Setup_](francais.md#setup-mohist)_._

Note : le mod suivant est nécessaire pour activer l'IP BungeeCord sur Forge sans SpongeForge \(comme SpongeForge est incompatible avec Cubic Chunks\).

1. Téléchargez la dernière version de SpeedBoost depuis [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/).
2. Placez le fichier que vous venez de télécharger dans votre dossier de `mods` et redémarrez le serveur.
3. Trouvez la section `bungeecord` dans `config/speedboost_config.json` et changez `state` en `true`.

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. Redémarrez votre serveur.
5. C'est fait ! Vous pouvez maintenant suivre au [Proxy Setup](francais.md#setup-proxy).

## Setup Proxy

_Si votre proxy Waterfall est hébergé par quelqu'un d'autre \(par exemple, si vous utilisez un serveur qui fait partie du Grand Network BuildTheEarth \), alors c'est déjà fait pour vous._

Ce guide suppose que vous avez déjà un proxy Waterfall en fonctionnement. Si vous avez un proxy BungeeCord, simplement [téléchargez la dernière version de Waterfall](https://papermc.io/downloads#Waterfall) et remplacez le avec le jar BungeeCord. Si vous n'avez aucun proxy, suivez le [setup guide officiel](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html) et configurez-le pour se connecter au serveur Forge.

### Setup Waterfall

Note: jusqu'à ce que[ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138) soit fusionné, il n'y a pas de téléchargement officiel pour ViaVersion.

1. Changez `forge_support` en `true` dans `config.yml`.

   ```text
   forge_support: true
   ```

2. Changez `ip_forward` en `true` dans `config.yml`.

   ```text
   ip_forward: true
   ```

3. Téléchargez les fichiers suivant :  

   Geyser depuis [Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)  

   ViaVersion depuis [here](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)  

   _Recommandé :_ Floodgate depuis[Jenkins](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _Optionel :_ ViaBackwards depuis[Jenkins](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _Optionel :_ ViaRewind depuis[Jenkins](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

4. Placez tous les fichiers téléchargés dans le dossier `plugins`de Waterfall puis redémarrez Waterfall.
5. Changez `suppress-conversion-warnings` en `true` dans `plugins/ViaVersion/config.yml`.

   ```text
   # Nous vous prévenons qu'il y a une erreur de conversion d'items et d'info de blocks entre les versions, devons nous résoudre ce problème ? (Seulement si c'est très suggéré souvent)
   suppress-conversion-warnings: true
   ```

6. Changez `general-thread-pool` en le nombre de coeurs sur votre server Waterfall dans `plugins/Geyser-BungeeCord/config.yml`. Exemple pour 8 coeurs :

   ```text
   # Thread pool size
   general-thread-pool: 8
   ```

7. Changez `cache-chunks` en `true` dans `plugins/Geyser-BungeeCord/config.yml`. ne tenez pas compte des mises en garde, ce paramètre est essentiel pour faire marcher les clients Bedrock correctement avec Cubic Chunks.

   ```text
   # Configurez si le chunk cache est activé ou pas. Cela garde une trace que chaque joueur charge.
   # bien que ce paramètre permet certaines choses comme l'animation de cassage de block texture en créatif
   # par exemple mais il est TRÈS recommandé de désactiver le paramètre car il utilise beaucoup de RAM.
   # Pourtant, quand vous utilisez la version Spigot de Geyser, il supporte les caractéristiques ou
   # implémentations qui l'activent automatiquement sans cache ajouté come Geyser a un accès direct au
   # serveur.
   cache-chunks: true
   ```

8. _Si vous téléchargez Floodgate :_ Trouvez la section `player-link` dans `plugins/floodgate-bungee/config.yml` et changez `enable` en `true`.

   ```text
   # Type d'authentication : peut-être hors-ligne, en ligne ou floodgate (regardez https://github.com/GeyserMC/Geyser/wiki/Floodgate).
   auth-type: floodgate
   ```

9. _Si vous téléchargez Floodgate:_ Trouvez la section `remote` dans `plugins/Geyser-BungeeCord/config.yml` et changez `auth-type` en `floodgate`.

   ```text
   # Qu'il s'aggisse d'activer le système de mise en relation(link), désactiver cette fonctionnalité
   # empêchera les joueurs d'utiliser la fonctionnalité même s'ils étaient déjà reliés. 
   enable: true
   ```

10. Redémarrez Waterfall.

Bravo ! Vous pouvez maintenant vous connectez avec votre serveur Cubic Chunks à travers Waterfall avec un de ces clients :

* Cubic Chunks 1.12.2
* Vanilla Édition Java 1.12.2-1.16.3
* Édition Bedrock 
* _Si vous avez téléchargé ViaBackwards :_ Vanilla Édition Java 1.9-1.16.3
* _Si vous avez téléchargé ViaRewind :_ Vanilla Édition Java 1.7-1.16.3

## Notes Additionelles :

### ViaRewind et BungeeTabListPlus

Si vous utilisez ViaRewind avec BungeeTabListPlus sur Waterfall, créer un nouveau fichier `1-7-10.yml` dans`plugins/BungeeTabListPlus/tabLists` avec contenu le text suivant :

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

C'est important pour éviter de "casser" les skins des joueurs et les name tags au-dessus des joueurs pour les client de 1.7.10 et moins.

