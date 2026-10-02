# NGUInjector (Chinese fork)

Steve's fork `SteveWang92/NGUInjector-Chinese` of `yuigahama0rf/NGUInjector-Chinese`, itself a
Chinese localization of `rus9384/NGUInjector`. It is an automation mod for the Steam game NGU IDLE,
injected into the running game's Mono runtime. Kept for study and personal use; it has no releases.

## Branches and upstream

- `main` mirrors `upstream/main` exactly and only ever fast-forwards to it. Steve's own work lives
  on `dev`; feature branches are cut from `dev`.
- To take upstream changes: fast-forward `main` to `upstream/main`, then merge `main` into `dev`.
- No `changedeck.json`; nothing here is tagged or released.

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
