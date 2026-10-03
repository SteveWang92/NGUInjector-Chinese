# NGUInjector (Chinese fork)

Steve's fork `SteveWang92/NGUInjector-Chinese` of `yuigahama0rf/NGUInjector-Chinese`, itself a
Chinese localization of `rus9384/NGUInjector`. It is an automation mod for the Steam game NGU IDLE,
injected into the running game's Mono runtime. It stays a GitHub fork and is released as Steve's
own project, continuing the upstream version line from 4.1.7.

## Branches and upstream

- `main` is the release branch and moves only through the `dev` → `main` release PR, merged with a
  merge commit so the public `dev` history stays reachable from `main`. Steve's own work lives on
  `dev`; feature branches are cut from `dev`.
- To take upstream changes: fetch `upstream` and merge `upstream/main` into `dev` with a merge
  commit. This upstream sync is the one merge commit allowed besides the release merge.
- Releases go through `changedeck` (`changedeck.json`). The only version field is `Version` in
  `NGUInjector/Main.cs`, which the settings form displays. The `v4.1.7-cn.*` tags are
  `yuigahama0rf`'s releases and stay as upstream history.
- The release package is built and attached by hand after `ship`; `afterShip` in
  `changedeck.json` owns the steps.

## Terminology

- UI, `README.zh-CN.md` and `USAGE.zh-CN.md` use one Chinese term per game concept. Titan and zone
  names follow the third-party Chinese patch the localization was built against. Other fixed
  choices: Beast Mode 野兽模式, Boost stays `Boost`, Infinity Cube 魔方, Major/Minor Quest
  主要/次要任务, MacGuffin 麦高芬 (Guff A/B 麦高芬 α/β), Number 增数, ITOPOD 无尽之怒塔.
- Profile JSON keys and priority codes stay English.

## Build

- Build with the Visual Studio MSBuild (`D:\Program Files\Microsoft Visual Studio\18\Community\
  MSBuild\Current\Bin\MSBuild.exe`) and `/restore /p:Configuration=Release` on
  `NGUInjector/NGUInjector.csproj`. Unity references come from NuGet; `Assembly-CSharp.dll` is the
  game's own copy committed beside the project.
- The game's `Assembly-CSharp.dll` has not changed since 2021; if a game update ever changes it,
  replace the committed copy with the one from `NGUIdle_Data\Managed` before building.

## Run

- The run folder is `H:\NGU Idle\NGUInjector`: `inject.bat` plus `injector\` holding `smi.exe`,
  `SharpMonoInjector.dll` (both built from `warbler/SharpMonoInjector` source) and
  `NGUInjector.dll`. It does not need to be inside the game folder.
- Deploy by copying `NGUInjector/bin/Release/NGUInjector.dll` into `injector\`, restarting the
  game, then running `inject.bat` with the game open. A loaded copy cannot be replaced in place.
- Huorong flags the injector and deletes `SharpMonoInjector.dll` (including MSBuild intermediates)
  anywhere outside its trust zone. This repository and the run folder are trusted; build the
  injector inside one of them.
- Settings, profiles and logs live in `%UserProfile%\AppData\LocalLow\NGUInjector`; first-run
  settings have every automation disabled.

## Game data

- Saves are in `%UserProfile%\AppData\LocalLow\NGU Industries\NGU Idle`, base64 `BinaryFormatter`
  `SaveData { playerData, checksum }` where the checksum is the unkeyed MD5 of `playerData`. The
  game has no anti-cheat; edited values can unlock Steam achievements, and saves sync to Steam
  Cloud.
- Steam microtransaction purchases (real-money AP packs) are out of scope for any change here.
