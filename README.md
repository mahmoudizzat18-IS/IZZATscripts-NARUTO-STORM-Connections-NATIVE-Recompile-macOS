# IZZATscripts Connections Builder

A one-file Mac app that builds **Naruto x Boruto: Ultimate Ninja Storm Connections** as a native Apple silicon Mac app from your own game files.

The builder is attached to the [latest release](../../releases/latest) as `STORM-Connections-Builder.zip`.

> You must supply your own legally dumped game files and your own console keys. None are included.
![Builder](https://github.com/mahmoudizzat18-IS/IZZATscripts-Connections-Builder/blob/main/Builder.png?raw=true)
![Graphics](https://github.com/mahmoudizzat18-IS/IZZATscripts-Connections-Builder/blob/main/Graphic%20Option.png?raw=true)
![Controller](https://github.com/mahmoudizzat18-IS/IZZATscripts-Connections-Builder/blob/main/Controller%20Option.png?raw=true)
## Requirements

| Need | Details |
| --- | --- |
| Mac | Apple silicon (M1 or later) |
| macOS | A recent macOS with Metal 3 |
| Xcode | Full Xcode (not only the Command Line Tools), with the **Metal Toolchain** component installed |
| .NET | **.NET 10 SDK** (used by the shader translator) |
| Python | Python 3 (comes with Xcode's command line tools) |
| Disk space | About **20 GB** free for the build cache, plus room for the finished app |
| Keys | Your own `prod.keys`, placed at `~/.switch/prod.keys` |
| Game files (EU) | Base game `01005A20190A6000` (NSP, XCI, NSZ or XCZ) |
| | Update **1.7.0** (`v655360`), recommended |
| | Any DLC NSPs, optional |

### Installing the tools

1. Install **Xcode** from the App Store and open it once to accept the license.
2. Install the Metal Toolchain:
   ```bash
   xcodebuild -downloadComponent MetalToolchain
   ```
3. Install the **.NET 10 SDK** from https://dotnet.microsoft.com/download (or `brew install --cask dotnet-sdk`).
4. Put your keys in place:
   ```bash
   mkdir -p ~/.switch && cp /path/to/prod.keys ~/.switch/prod.keys
   ```

## Building the game

1. Download `STORM-Connections-Builder.zip` from the release and unzip it.
2. Move **STORM Connections Builder.app** anywhere, for example to `/Applications`.
3. The first time, right-click the app and choose **Open** (it is signed only on your Mac, not by Apple).
4. Click **Browse** and select:
   - the EU base game,
   - the EU 1.7.0 update,
   - any DLC you want.
5. Click **Install**. The build runs and shows its progress. The first build takes a while and uses about 20 GB of cache in `~/Library/Application Support/Storm Connections Builder/work`.
6. When it finishes, the game is in `/Applications/Naruto x Boruto Ultimate Ninja Storm Connections .app`. If a copy was already there, it is kept as a backup.

On first launch the builder copies its tools to `~/Library/Application Support/IZZATscripts Connections Builder/`. Builds run from there, because macOS doesn't allow writing inside a signed app.

## Tips

- **60 FPS:** builds from the EU 1.7.0 update use the game's 60 FPS mode. The Switch patch is by M0chila: <https://gbatemp.net/threads/naruto-x-boruto-ultimate-ninja-storm-connections-60-fps-mod-v1-7-0.684554/>
- **Sharper picture:** in the game's launcher, start with **MetalFX**, **2560x1440** output and **FXAA off**. Try 3840x2160 if the game holds 60 FPS. The game renders at 1920x1080, and MetalFX upscales it.
- **Black screen but sound plays:** quit the game and its launcher. In Terminal, run `bash "Repair-Installed-Game.command"` from `~/Library/Application Support/IZZATscripts Connections Builder/`. It repairs the installed game without rebuilding.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| "No prod.keys" | Put your keys at `~/.switch/prod.keys`. |
| Metal or shader compile errors | Install the Metal Toolchain (see above) and make sure `xcode-select -p` points to Xcode.app. |
| `dotnet` not found | Install the .NET 10 SDK and open a new Terminal. |
| The app won't open ("damaged" or "unidentified developer") | Right-click the app and choose **Open**, or run `xattr -cr "STORM Connections Builder.app"`. |
| Out of disk space | Free about 20 GB, or delete the old cache in `~/Library/Application Support/Storm Connections Builder/work`. |
