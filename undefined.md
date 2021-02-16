# 한국어

![](.gitbook/assets/serverguide.png)

이 가이드를 읽기 전, 제대로 된 마인크래프트 Forge 서버와 Cubic Chunks 모드가 있는지 확인해주세요.

시작하기 전: 서버 `mods` 폴더에서 Cubic Chunks 모드 외의 모든 "클라이언트 모드"들은 _전부_ 빼주세요. 만약 "클라이언트 모드"가 하나라도 존재한다면, 모드를 아예 쓰지 않는 바닐라 클라이언트들은 서버에 접속할 수 없게 됩니다.

## 서버 설정

1. [Jenkins](https://jenkins.daporkchop.net/job/Minecraft/job/CubicChunks/)에서 `CubicChunks-<버전>-SNAPSHOT-all.jar` 와 같이 되어 있는 최신 버전의 Cubic Chunks 모드를 다운로드 받아주세요.

   ![image](https://i.daporkchop.net/ulOLOAri.png)

2. 서버 `mods` 폴더에 있는 Cubic Chunks 모드 파일을 다운로드한 파일로 교체한 다음, 서버를 재시작해주세요.
3. `config/cubicchunks.cfg` 파일에서 `allowVanillaClients`의 값을 다음과 같이 `true`로 설정해주세요.

   ```bash
    # Allows clients without cubic chunks to join. THIS IS INTENDED FOR VANILLA CLIENTS. This is VERY likely to break when used with other mods
    B:allowVanillaClients=true
   ```

   이제 1.12.2 자바 바닐라 클라이언트들도 서버로 접속할 수 있게 되었습니다. 만약 베드락 클라이언트들도 서버에 접속할 수 있도록 하고 싶으시다면 계속 읽어주시고, 아니면 여기서 마치시면 됩니다.

4. `server.properties` 파일에서 `online-mode`의 값을 다음과 같이 `false`로 설정해주세요.

   ```text
   online-mode=false
   ```

   이제부터 만약 실행해고 있는 서버가 Mohist 서버라면 [Mohist 설정](undefined.md#mohist)으로 가주시고, 아니면 [Forge 설정](undefined.md#forge)으로 가주세요.

### Mohist 설정

_다음은 Mohist 서버만을 위한 설명서입니다. 만약 Mohist 서버를 사용하고 있지 않으시다면_ [_Forge 설정_](undefined.md#forge)_으로 넘어가주세요._

1. [Jenkins](https://ci.codemc.io/job/Mohist-Community/job/Mohist-1.12.2/lastSuccessfulBuild/artifact/projects/mohist/build/libs/)에서 최신 버전의 Mohist를 다운로드 받아주세요.
2. 서버 폴더 내의 Mohist.jar 파일을 1. 에서 다운로드 받은 것으로 교체해주시고, 필요하시다면 이름도 바꿔주세요.
3. `spigot.yml` 파일에서 `bungeecord` 값을 다음과 같이 `true`로 설정해주세요.

   ```text
   bungeecord: true
   ```

4. 서버를 재시작해주세요.
5. 다 됐습니다! 이제 [프록시 설정](undefined.md#proxy)으로 넘어가주시면 되겠습니다.

### Forge 설정

_다음은 Mohist 서버가 **아닌** 서버만을 위한 설명서입니다. 만약 Mohist 서버를 사용 중이시라면_ [_Mohist 설정_](undefined.md#mohist)_로 돌아가주세요._

참고: SpongeForge는 Cubic Chunks 모드를 지원하지 않으므로 다음 모드를 사용할 때 SpongeForge를 빼주세요.

1. [Jenkins](https://jenkins.daporkchop.net/job/PorkStudios/job/SpeedBoost/job/master/lastSuccessfulBuild/artifact/build/libs/)에서 최신 버전의 SpeedBoost를 다운로드 받아주세요.
2. 서버 `mods` 폴더에다가 1. 에서 다운로드받은 SpeedBoost를 넣어주시고 서버를 재시작해주세요.
3. `config/speedboost_config.json` 파일에서 다음과 같이 `bungeecord` 안에 있는 `state` 값을 `true`로 설정해주세요..

   ```javascript
   "bungeecord": {
    "state": true
   },
   ```

4. 서버를 재시작해주세요.
5. 다 됐습니다! 이제 [프록시 설정](undefined.md#proxy)으로 넘어가주시면 되겠습니다.

## 프록시 설정 <a id="proxy"></a>

_만약 서버의 Waterfall 프록시가 누군가에 의해 이미 호스팅되고 있다면, 여기서 마치셔도 됩니다._

이 다음부터는 현재 당신이 Waterfall 프록시를 설정해서 실행하고 있다는 가정 하에 설명을 해줄 겁니다. 그래서 이 다음으로 넘어가기 전, 만약 이미 BungeeCord 프록시가 있으시다면 간단히 [최신 버전의 Waterfall을 다운로드 받은 다음](https://papermc.io/downloads#Waterfall) BungeeCord.jar와 바꿔주시고, 아무 프록시도 존재하지 않다면 [Waterfall 공식 설정 가이드](https://paper.readthedocs.io/en/latest/waterfall/getting-started.html)를 읽어주신 다음 Waterfall 프록시가 Forge 서버와 연결되도록 설정을 먼저 해주세요.

### Waterfall 설정

참고: [ViaVersion/ViaVersion\#2138](https://github.com/ViaVersion/ViaVersion/pull/2138)이 메인 ViaVersion과 병합될 때까지 공식적인 ViaVersion 다운로드 소스는 없을 것입니다.

1. `config.yml` 파일에서 `forge_support` 와 `ip_forward` 의 값을 다음과 같이 `true`로 설정해주세요.

   ```text
   forge_support: true
   # ...
   ip_forward: true
   ```

2. 다음 Waterfall 플러그인들을 다운로드 받아주시고, 모두 Waterfall의 `plugins` 폴더에 넣은 다음 Waterfall을 재시작해주세요.

   [Geyser](https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/bungeecord/target/)

   [ViaVersion](https://cdn.discordapp.com/attachments/295539008891518977/766749691949744138/ViaVersion-3.2.0-SNAPSHOT.jar)

   _권장:_ [Floodgate](https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/development/lastSuccessfulBuild/artifact/bungee/target/)  

   _선택 1:_ [ViaBackwards](https://ci.viaversion.com/view/ViaBackwards/job/ViaBackwards/lastSuccessfulBuild/artifact/all/target/)  

   _선택 2:_ [ViaRewind](https://ci.viaversion.com/view/ViaRewind/job/ViaRewind/lastSuccessfulBuild/artifact/all/target/)

3. `plugins/ViaVersion/config.yml` 파일에서 `suppress-conversion-warnings` 값을 다음과 같이 `true`로 설정해주세요.

   ```text
   # We warn when there's a error converting item and block data over versions, should we suppress these? (Only suggested if spamming)
   suppress-conversion-warnings: true
   ```

4. `plugins/Geyser-BungeeCord/config.yml` 파일에서 `general-thread-pool` 값을 Waterfall 서버의 코어 수에 맞게 설정해주세요. 예를 들어서 8 코어일 때:

   ```text
   # Thread pool size
   general-thread-pool: 8
   ```

5. `plugins/Geyser-BungeeCord/config.yml` 파일에서 `cache-chunks` 값을 `true`로 설정해주세요. \(참고로 베드락 클라이언트들이 Cubic Chunks 모드와 잘 작동하기 위해서 값을 다음과 같이 설정한 것이므로 밑에 적혀있는 경고문은 무시해주세요.\)

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

6. _Floodgate를 다운로드 받으셨다면:_ `plugins/floodgate-bungee/config.yml` 파일에서 다음과 같이 `player-link` 안에 있는 `enable` 값을 `true`로 설정해주세요.

   ```text
   # Whether to enable the linking system. Turning this off will prevent
   # players from using the linking feature even if they are already linked.
   enable: true
   ```

7. _Floodgate를 다운로드 받으셨다면:_ `plugins/Geyser-BungeeCord/config.yml` 파일에서 다음과 같이 `remote` 안에 있는 `auth-type` 값을 `floodgate`로 설정해주세요.

   ```text
   # Authentication type. Can be offline, online, or floodgate (see https://github.com/GeyserMC/Geyser/wiki/Floodgate).
   auth-type: floodgate
   ```

8. Waterfall을 재실행해주세요.

축하드립니다! 이제 다음 클라이언트들로 \(Waterfall을 통해서\) Cubic Chunks 모드 서버로 접속하실 수 있게 되셨습니다.

* Cubic Chunks 모드 1.12.2
* 바닐라 Java 에디션 1.12.2 ~ 1.16.3
* 베드락 에디션
* _ViaBackwards를 다운로드 받으셨다면:_ 바닐라 Java 에디션 _1.9_ ~ 1.16.3
* _ViaRewind를 다운로드 받으셨다면:_ 바닐라 Java 에디션 _1.7_ ~ 1.16.3

## 추가 내용

### ViaRewind과 BungeeTabListPlus

만약 Waterfall에서 ViaRewind를 BungeeTabListPlus와 함께 사용하신다면 `plugins/BungeeTabListPlus/tabLists` 폴더에서 새로운 파일 `1-7-10.yml`을 만드시고, 내용을 다음과 같이 적어주세요.

```text
showTo: ${viewer client_version_below_1_8}
priority: 100000

showHeaderFooter: false
type: HEADER_FOOTER
```

이 작업을 해주셔야 1.7.10 이하의 플레이어 스킨들이 깨지는 것을 방지할 수 있습니다.

