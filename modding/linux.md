<!-- TITLE: Linux Modding Guide -->
<!-- SUBTITLE: Getting started on Beat Saber mods for Linux! -->

# How to install mods

## Preface 

Most Beat Saber mod installers weren't built to run on Linux, so we have to do some small things to get it to work on Linux.
It is very similar to a Windows install, but you will need some workarounds.

>Using mods in Linux isn't supported by mod developers, so you might encounter bugs!
{.is-warning}

## Using Wine and Winetricks

> **Run the game at least once** before trying to mod the game! This applies to reinstalling your game too.
{.is-danger}

Make sure you have [Wine](https://wiki.winehq.org/Download) and [Winetricks](https://github.com/Winetricks/winetricks/blob/master/README.md) installed before starting.

1. Make a new 32-bit Wine prefix.
```bash
>  $ export WINEARCH="win32"
>  $ export WINEPREFIX=~/.winemods
>  $ wineboot -u
```
2. Install the dotnet472 package using winetricks. If it asks to restart choose 'Restart later'.
```bash
>  $ winetricks dotnet472
```

![dotnet472](https://i.imgur.com/r62nmZW.png)

> There will be multiple install prompts you will have to go through, this is normal!
{.is-warning}

3. Download a [mod installer](https://bsmg.wiki/beginners-guide#installers) and put it in your [install folder](https://bsmg.wiki/faq/install-folder).
![Install Folder](https://i.imgur.com/ap2ofvE.png)
4. Move your Beat Saber folder onto your desktop and open a terminal
5. Navigate to your Beat Saber folder in a terminal and run your installer in Wine.
```bash
>  $ cd Desktop
>  $ cd "Beat Saber"
>  $ wine BeatSaberModManager.exe
```

![BeatSaberModManager](https://i.imgur.com/sXUhA8x.png)

4. Direct the installer to your Beat Saber directory
![BeatSaberModManager](https://i.imgur.com/DzEaDaI.png)
5. Install your mods. You should now have a Plugins folder.
6. Close out of the installer and put the Beat Saber folder back into common.
![Beat Saber folder](https://i.imgur.com/xWeN0TT.png)
7. Start Beat Saber and check if the mods are installed. If they aren't you may need to [do a Dll override](/modding/linux#dll-override)

## Using a Virtual Machine

> **Run the game at least once** before trying to mod the game! This applies to reinstalling your game too.
{.is-danger}

Make sure you have [VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads) installed before starting.

1. Download a [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10ISO)
2. Make a new Windows 10 virtual machine and start it.
![VirtualBox](https://i.imgur.com/HJMwMSr.png)
3. When asked, select the Windows 10 ISO. and start it.
![VirtualBox](https://i.imgur.com/af0ikmV.png)
4. After you are finished installing Windows, download a [mod installer](beginners-guide#installers) inside the VM.
![ModAssistant Install](https://i.imgur.com/juZzw1j.png)
5. Make a shared folder by going to 'Devices > Shared Folders > Shared Folder Settings...'.
Make a new shared folder with the common folder '/.local/share/Steam/steamapps/common/' and turn Auto-mount on.
![Shared Folder](https://i.imgur.com/FoV8BE3.png)
![Shared Folder](https://i.imgur.com/rcpnROc.png)
6. Run the mod installer you have downloaded, and manually select your Beat Saber folder, then install your mods.
7. Exit the VM and start Beat Saber. Your mods should be installed. If they aren't, go to [Dll Override](linux#dll-override)

## Dll Override

Wine doesn’t use DLLs the same way Windows does, so you have to change a few things to make the IPA injection work.

> Messing with registry files can be dangerous, make sure you don't touch anything besides what the guide tells you to.
>
> If you messed up the registry file, either verify your game files or reinstall Beat Saber after backing up your files.
{.is-danger}

1. Navigate to '/.local/share/Steam/steamapps/compatdata/620980/pfx/' and open 'user.reg'
2. Inside the file, navigate to [Software\\Wine\\DllOverrides]. Try Ctrl + F and type DllOverrides to get there quicker
3. Paste `"winhttp"="native,builtin"` on the bottom below the others, and save the file.

![DllOverrides](https://i.imgur.com/dgemtef.png)

## SongCore breaks custom songs

If loading SongCore causes you to be unable to play any custom songs, try creating a folder that isn't done automatically:

```bash
>  $ cd "~/.local/share/Steam/steamapps/compatdata/620980/pfx/drive_c/users/steamuser/Local Settings"
>  $ mkdir -p "LocalLow/Hyperbolic Magnetism/Beat Saber"
```

Of course, change `~/.local/share/Steam/steamapps/` to the location of the Steam library that you have installed Beat Saber to.

# Have questions?
Visit the [FAQ](faq) or drop by the #support tab in the [discord](https://discord.gg/beatsabermods)!
