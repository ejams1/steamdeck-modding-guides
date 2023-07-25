# Wabbajack - Root Builder

Root Builder is a tool that authers can use to build mod lists that don't actually get installed to or touch the base game folder (i.e. where you installed your game).

> **Note**
> We will NOT be using Mod Organizer 2 on the Steam Deck and we will be overwriting the base game folder. This means you can only have ONE list installed at a time.

For this example, I will be using the `Fallout: New Vegas` list [Begin Again](https://www.nexusmods.com/newvegas/mods/79547) but this guide should be applicable to _any_ list that uses Root Builder.For example, I have also used these steps for the `Oblivion` list `Last Seed`.

## Prerequisites

- Ensure that whichever game you are modding is installed on the internal SSD (not an SD card) and you have launched it at least once
- For Proton version, I would recommend whatever is the latest `Proton-GE` at the time as it will include the latest patches and enhancements and should maximize compatibility and performance for most games. At the time of writing, this is `Proton-GE 8-6`. You can install it via an app called `ProtonUp-Qt` which you can get in the app store on the deck. Once installed, you simply need to navigate to Steam -> Your Game -> Properties -> Compatibility and choose the Proton-GE version you just installed

## Install Guide

1. Follow the installation guide for your list on your Windows machine and make sure it works correctly; in this case, the guide for the `Begin Again` can be found [at the bottom of its Nexus Mods page](https://www.nexusmods.com/newvegas/mods/79547).
2. Edit the ini files provided by your list to change the resolution to match the Steam Deck's; these settings should be the same for all Bethesda games:

```text
iSize W=1280
iSize H=800
```

Make any other ini changes you'd like as well before we move the files to the Steam Deck.

3. Open Mod Organizer 2 and select the drop-down next to the `Run` button, and click `<Edit...>`. Click `Add from file...` and navigate to the modlist install folder -> `explorer++` and select `Explorer++.exe`. Before we apply this, add the path to your `Fallout New Vegas` data folder to the `Add Arguments` box - in my case, that would be `"G:\SteamLibrary\steamapps\common\FalloutNV"` (double quotes included). This isn't necessary but will automatically open up the game directory when wwe launch this tool rather than us having to navigate here manually.
    - The tool we just set up, `Explorer++`, allows us to see what the game folder looks like when you execute the game from Mod Organizer 2. Recall that because our list uses Root Builder, it doesn't actually touch the original game installation, so when you run the list, it virtualizes the directory and includes the mod content. Think of this like it dynamically moving the modded content into the game install directory at runtime, and removing it when you quit.
4. Now that we have set up the executable for `Explorer++`, choose it from the drop-down and run it. You should be brought to the game installation folder, but now it should contain extra files from your modlist. This is what we want to copy over to the Steam Deck and overwrite the game installation there with, but to do that we need to copy everything out of here and into an intermediate folder. As discussed above, this is because once we close `Explorer++`, the game folder will not contain all of the mod content.
5. In the virtual file system, it shows the entire modlist put together as if though everything from the modlist was dropped into the game install directory, so we want to copy the whole thing out to a temporary location (i.e. on your desktop make a directory called `begin-again-extracted`) and copy that over to the steam deck; I prefer to use SSH and login to the deck with WinSCP but it doesn’t matter how you do it
    - If you mess around and get lost in explorer++ and cant get back to the directory, it was just open to the install folder for you Fallout New Vegas

> **Warning**
> Linux treats folders with different casing (`data` vs. `Data`) as different folders, but Windows doesn’t. When copying over to the steam deck, make sure the casing is the same for the Data folder (it is lower case in the `Begin Again` installation). Alternatively, you can delete the contents of the game installation folder on your steam deck as all of the game files will be copied over along with the mod content, so that is probably the safer way to do it.

6. Next, go into your `C:\Users\<YOURUSERNAME>\AppData\Local\FalloutNV` and copy the `plugins.txt` over to the deck. It needs to go into the equivalent spot on the deck which is in `$HOME/.steam/steamapps/compatdata/22380/c_drive/users/steamuser/AppData/Local/FalloutNV`. If you are installing a list for another game, you need to find the steam game ID for it - simply googling `steam gameid <game name>` will bring you the answer.
7. Next, copy over the `ini`s you modified (originally from the `profiles` folder) to the equivalent place on the deck: `$HOME/.steam/steamapps/compatdata/22380/c_drive/users/steamuser/Documents/My Games/FalloutNV`
    - Ensure that the ini setting `sD3DDevice=` is set to something, otherwise it will boot-loop. I left mine to what it was on my desktop (`sD3DDevice="NVIDIA GeForce RTX 3080"`) and that worked, so it doesn't need to specifically match the APU name of the steam deck
8. Bethesda games prior to `Skyrim SE`/`Fallout 4` determined their load order by looking at the modified date of the plugins to determine load order, so while you need the plugins.txt file to tell the game _which_ mods to load, you also need to ensure the mods in your list have been modified in the order of your load order. If you had loaded the list in mod organizer 2 as you should have to test it out, then this will already be done for you although you can double-check by opening the `Data` folder and sorting by modified date to see if the plugins are correct
9. Rename the `falloutNVLauncher.exe` to `falloutNVLauncher.exe.backup` and then rename the `nvse_launcher.exe` to `falloutNVLauncher.exe` - this will allow you to launch new vegas through steam. The same applies to other Bethesda games which all have their own respective launchers

At this point, the mod list should be functional on your steam deck! If you encounter performance issues, you can try a few things:

- Verify that the modlist is not performance-heavy on a regular desktop! Many modlists are designed to push the visuals of these games significantly past what they originally were, and that does not bode well for steam deck performance
- Lower the visual settings in the inis
- Make sure to apply all of the recommended tweaks in CryoUtilities
- Drop the refresh rate to 40Hz and set the FPS cap to 40FPS in the steam deck game profile; this is much smoother than 30 but not as demanding as 60 and the steam deck natively supports 40Hz
- Enable `Allow Tearing` in the steam deck game profile - this will reduce input latency which makes it easier to aim since these games are first-person
- You can try using `Variable Rate Shading` and/or using `FSR` in the steam deck game profile as other ways of trying to increase performance, but they may impact the visuals
- Drop the resolution (steam deck is native 1280x800, try dropping it below that but make sure to keep it a 16:10 aspect ratio if you would like to avoid black bars at the top and bottom of the screen)
- Disable SMT (hyperthreading) using the `PowerTools` decky plugin as SMT is currently bugged in the steam deck - this is apparently going to be fixed in SteamOS 3.5
  - This is NOT recommended for Skyrim SE/Fallout 4 as the creation engine seems to utilize the extra threads better than older Bethesda games
- You can try manually pinning the CPU/GPU frequencies high or low depending on where the bottleneck is (i.e. lower the CPU frequency to allow more power to go to the GPU in GPU-limited scenarios)
