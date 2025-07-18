<div align="center">
  <div><h1>Diablo II • Median XL • Launcher</h1></div>
  <div><img width="80" src="./../res/icon.svg" /></div>
  <div><a href="https://github.com/murkl/d2launcher/releases/latest"><b>Download</b></a></div>
  <div><img src="./screenshot.png" /></div>
  <div><p><img src="https://img.shields.io/badge/MAINTAINED-YES-green?style=for-the-badge" /></p></div>
</div>

# Features

- Simple Backup & Restore (Savegames & Diablo II Installation)
- User Tweaks (Auto Install Scripts for Plugins etc.)
- Custom Proton (64 Bit) build will download by script
- Download latest Median XL patch (incl. notification on new updates)
- Median XL Version Management
- Import/Export of savegames
- [D2 Stats](https://github.com/Zahariel1942/D2Stats/) included (will download by script)
- [Sven's Glide wrapper](http://www.svenswrapper.de) included
- Direct Draw [cnc-ddraw](https://github.com/FunkyFr3sh/cnc-ddraw) supported
- Diablo II 1.13c files to work with Median XL included
- Updater (incl. notification on new updates)
- Supports the execution of EXE files within the wine prefix
- Configurable (see [Documentation](#documentation))
- Shellcheck approved
- 100% GUI

# Installation

You need the Diablo II installation files for the script to work! (You will be asked for the location in the script)

## Arch Linux

- Install from AUR
  - [aur/d2launcher](https://aur.archlinux.org/packages/d2launcher)

## Debian/Ubuntu/elementaryOS

- Download & Extract: <a href="https://github.com/murkl/d2launcher/releases/latest"><b>d2launcher.tar.gz</b></a>
- Install Dependencies
  - `sudo apt install wine zenity curl unzip jq wmctrl fuse2 xdelta3`
  - Some distros label fuse2 as libfuse2, if you receive an error about fuse2 not being found, try libfuse2
- Run
  - `./d2launcher`

## Pop_OS!

- Download & Extract: <a href="https://github.com/murkl/d2launcher/releases/latest"><b>d2launcher.tar.gz</b></a>
- Install Dependencies
  - `sudo apt install wine zenity curl unzip jq wmctrl fuse2 ruby-notify xdelta3`
  - Some distros label fuse2 as libfuse2, if you receive an error about fuse2 not being found, try libfuse2
- Run
  - `./d2launcher`

# Documentation

You can override the script properties in the configuration settings (`Settings` > `Edit Configuration`). These settings can be edited manually in `~/.d2launcher/d2launcher.conf`.

<sub><b>Example `d2launcher.conf`:</b></sub>

```
d2_dir="/path/to/diablo/installation"
d2_exe="Diablo II.exe"
d2_args="-ddraw"
wine_init="gamemoderun"
d2_stats_tray="true"
update_check="true"
mxl_update_check="true"
mxl_update_channel="public"
mxl_update_exclude=("d2gl.mpq" "glide3x.dll" "ddraw.dll" "cnc-ddraw config.exe")
gui_width="420"
gui_height="320"
tweaks_upstream="https://my/custom/url/to/tweaks.db"
```

## Backup & Restore

All files are located here: `~/.d2launcher`. Simply copy & paste to another system. The Diablo II binary files are stored here `~/.d2launcher/bin/diablo2`.

## Logging

The logging file is `~/.d2launcher/d2launcher.log` and **is** rotated on every start of d2launcher. This contains only logs from execution of Diablo II.

## Menu Custom command

Replace "Diablo II" menu command with `custom_command="/my/custom/cmd"` (e.g. to start via Lutris or custom script instead).

## Exclude files from update patch

Add this array property to exclude files from update
`mxl_update_exclude=("file1" "file2")`

Best when using tweaks:

```
mxl_update_exclude=("d2gl.mpq" "glide3x.dll" "ddraw.dll" "cnc-ddraw config.exe")
```

## Median XL Beta

Change the property `mxl_update_channel` from `public` to `beta`.

## Change Download URL's

```
wine_native_url="https://github.com/Kron4ek/Wine-Builds/releases/download/6.3-7-proton/wine-6.3-7-proton-amd64.tar.xz"
d2_stats_url="https://github.com/Zahariel1942/D2Stats/releases/latest/download/D2Stats.zip"
d2_sigma_loader_url="https://github.com/SyndromeDayna/diablo-2-median-xl-sigma-loader/releases/download/3/sigma-loader.exe"
tweaks_upstream="https://raw.githubusercontent.com/murkl/d2launcher/refs/heads/main/res/tweaks.db"
```

**Note:** If you change the URLs, you have to force the regarding update/install: `Update Manger` > `Force Proton Update`/`Force D2Stats Update`

## Custom Wine Version

If you use Wine you have to set `wine_user="$USER"` otherwise for Proton set to `wine_user="steamuser"`

```
wine_default="/path/to/your/custom/wine"
wineprefix="$HOME/my/custom/wine_prefix"
wine_user="steamuser"
```

## Theming

```
gui_width="360"
gui_height="280"
gui_font="UbuntuMono Nerd Font"
gui_color="#eeeeee"
gui_size="9"
gui_dialog_width="280"
gui_dialog_height="140"
gui_dialog_font="UbuntuMono Nerd Font"
gui_dialog_color="#aaaaaa"
gui_dialog_size="9"
```

## Using D2Stats

It's nessesary to start D2Stats (Statistics) in d2launcher first, before starting Diablo II. Because d2launcher will check every start of Diablo II (using pgrep) if D2Stats is running. In this case, d2launcher starts Diablo II automatically with [sigma-loader](https://github.com/SyndromeDayna/diablo-2-median-xl-sigma-loader).

## Using cnc-ddraw

Thanks to [@GnomeBeans](https://github.com/murkl/d2launcher/issues/8#issuecomment-1553762919)

1. Download latest [cnc-ddraw.zip](https://github.com/FunkyFr3sh/cnc-ddraw/releases)
2. Unzip the downloaded `cnc-ddraw.zip` and drop the content into `~/.d2launcher/bin/diablo2` install dir.
3. Goto `Settings` > `Wine Settings` > `Library` and override/add `ddraw` (set DLL load strategy to: `native then built in`).
4. Change `d2_args` property in `Settings` > `Edit Configuration` from `-3dfx` to `-ddraw`
5. Optimize prefered settings: `Settings` > `Direct Draw Settings` (optional)
6. Run `Diablo II`

## Using Game Mode / Hybrid Graphics

Install the `gamemode` package in your system and add this property in `Settings` > `Edit Configuration`:

```
wine_init="gamemoderun"
```

When using **Hybrid Graphics**, you can add for NVIDIA:

```
wine_init="prime-run gamemoderun"
```

## Diablo II arguments

Goto `Settings` > `Edit Configuration` and modify `d2_args` property:

```
Enable Glide wrapper       | -3dfx
Enable Direct Draw         | -ddraw
Window mode                | -w
Skip to Median XL Login    | -skiptobnet
No sound                   | -ns
```

**Note:** Add multiple arguments with `-ddraw -skiptobnet ...`

## User Tweaks

Open `Tweaks` in the main menu and select the desired tweak script that you want to install. This is intended for your own install scripts such as d2gl or cnc-ddraw.

### Update Tweaks Database

To update this shown tweak list, goto `Update Manager` > `Update Tweaks Database`. The file set in the `tweaks_upstream` property will be downloaded to `~/.d2launcher/tweaks.db` (or copied if `tweaks_upstream` is set to a local file).

### Tweaks Database Syntax

Separated by the two header lines `###!> tweak_name: ...` and `###!> tweak_version ...` (please keep this order), all tweak scripts are saved in one file.

The working directory is a generated temporary directory and is deleted after termination. You have access to the variables from `d2launcher.conf` within the tweaks script.

**Note:** The Diablo II installation dir is: `~/.d2launcher/bin/diablo2` (use this dir to copy d2-gl files for example)

<sub><b>Example `tweaks.db`:</b></sub>

- Create a new `~/tweaks.db`
- Set `tweaks_upstream="~/tweaks.db"`

**Note:** The `tweaks.db` file can be saved in any location. It must then be adapted accordingly in the `tweaks_upstream`.

```
###!> tweak_name: my_first_tweak_script
###!> tweak_version: 1.0.0
echo "You can use bash code to pimp your Diablo II here..."

###!> tweak_name: my_second_tweak_script
###!> tweak_version: latest
echo "Do another plugin stuff..."
```

**Note: Root access is not supported!**

### Share your own Tweaks Database

You need to share your URL to your `tweaks.db` and set as `tweaks_upstream` in settings. Remember to update the tweaks database to create new local `~/.d2launcher/tweaks.db` from `tweaks_upstream`.

**Note:** Feel free to open a PR and merge your tweaks into d2launcher as a PR.

## Glide Wrapper Settings (deprecated)

Change in `Settings` > `Glide Wrapper Settings` (optional)

### Settings

```
☐          window mode
☑          capture mouse
☐          keep aspect ratio
☐          vertical synchronization (VSYNC)
no         fps-limit
no         static size
☐          window extras
auto       refreshrate
☑          desktopresolution
```

### Renderer

```
32 MB       texture-memory
1024x1024   buffer-texture-size
☑           32 bit rendering
☑           texture for videos
☑           bilinear filtering
☑           supersampling
☑           shader-gamma
☐           no gamma
☑           keep desktop composition
```

### Extensions

```
☑           GL_EXT_vertex_array
☑           GL_ATI_fragment_shader
☑           GL_ARB_fragment_program
☑           GL_EXT_paletted_texture
☑           GL_EXT_shared_texture_palette
☑           GL_EXT_packed_pixels
☑           GL_EXT_texture_env_combine
☑           WGL_EXT_swap_control
☑           WGL_ARB_render_texture
```

# External Sources

Many thanks to these projects:

- https://median-xl.com
- https://github.com/Kron4ek/Wine-Builds/
- https://github.com/Kyromyr/D2Stats
- https://github.com/Zahariel1942/D2Stats/
- https://github.com/azadix/D2Stats
- https://github.com/SyndromeDayna/diablo-2-median-xl-sigma-loader
- https://github.com/synthagency/icons-flat-osx
- http://www.svenswrapper.de
- https://github.com/FunkyFr3sh/cnc-ddraw
- https://github.com/GavinK88/d2gl-mxl-1.0
