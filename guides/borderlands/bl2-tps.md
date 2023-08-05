# Borderlands 2 / The Pre-Sequel

There are 2 types of mods for Borderlands 2 / TPS:

- Text-based; these are the ones you'll see on Nexus Mods primarily, and will have you place a `patch.txt` in your `Binaries` directory such as the Unofficial Community Patch
- PythonSDK-based; these come as a folder containing Python scripts, and are typically found on the PythonSDK website

We will look at using both types of mods but given recent developments in the Borderlands scene, we don't need to do any sort of hex editing or even use the Borderlands Community Mod Manager (BLCMM). The PythonSDK supports both types of mods, so we just need to get that up and running and perform a few additional steps.

For the purposes of this guide, we will be installing the [Unofficial Community Patch](https://www.nexusmods.com/borderlands2/mods/50?tab=description) for Borderlands 2, but the procedure should be similar for other mods for BL2 or TPS.

0. Download the game fresh, and change the compatibility mode to use Proton Experimental or Proton-GE if you use that. Then launch the game once to make sure it installs the required Microsoft C++ redistributables.
1. Follow [the official guide](https://bl-sdk.github.io/#sdk-installation) to install the PythonSDK, including the subsequent section on using it in Linux (which is just setting the launch parameters).
2. After the PythonSDK is installed and your Steam launch parameters have been configured for Linux, download the PythonSDK mod called [Text Mod Loader from here](https://bl-sdk.github.io/mods/TextModLoader/). This adds support for text-based mods.
3. Extract the mod and copy the resulting folder to the Borderlands 2 / TPS install path into `Borderlands 2\Binaries\Win32\Mods`. This is where any PythonSDK mods will need to be installed to.
4. Next, download the latest Unofficial Community Patch file [from here](https://www.nexusmods.com/Core/Libs/Common/Widgets/DownloadPopUp?id=1045&game_id=428). In the download, you will see a file called `Patch.txt` - we need to copy this to the BL2 / TPS install path here: `Borderlands 2\Binaries`.
5. (OPTIONAL) If you would like to modify the features of the community patch, you will need to open it with the mod manager. There is now a newer one known as [OpenBLCMM](https://github.com/BLCM/OpenBLCMM) which has its own guide on how to install it on Linux. Simply open the `Patch.txt` file in the mod manager and you will see all of the options that you can enable/disable.
6. (OPTIONAL) The Unofficial Community Patch by default requires online connectivity to function. If you would like to play offline, download the PythonSDK mod [Offline Helpers](https://bl-sdk.github.io/mods/OfflineHelpers/) and install it similar to how we installed the Text Mod Loader above. Next, open the mod folder and open the file `__init__.py`, then change the `false` on line 31 to `true`. This will force the game to start in offline mode. Finally, you need to open the `Patch.txt` file for the Unofficial Patch, search for `GearboxAccountData_1` and change the `1` to a `0` - this will tell the mod to function in offline mode.
7. We now have the Unofficial Community Patch installed and configured, so we can try it out. Launch the game, and you should see a `Mods` section in the main menu. Open that and you should see the list of PythonSDK mods you have installed. There will be some default ones that come with it like Backpack Manager which you can choose to enable if you'd like. Scroll down and you should see `Text Mod Loader` - make sure to enable it by clicking on it, then do the same for `Patch.txt` which corresponds to the Unofficial Community Patch.
8. Finally, verify that the patch is installed and functioning correctly by launching into a game and navigating to the `Badass Rank` menu - you should see a banner at the bottom above the button legend that says `Running UCP 5.0.4`. If you didn't configure the mod for offline and you try running the game without internet, it will not work so please refer to step 6 if you would like to do that.

If you would like to install additional PythonSDK-based mods, [you can find them here](https://bl-sdk.github.io/mods/).
