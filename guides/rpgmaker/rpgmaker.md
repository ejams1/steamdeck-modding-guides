# RPG Maker Games

RPG Maker games may work already, but they might run poorly. For example, the game `Fear & Hunger` which is quite popular on the deck runs like garbage, frequently hitching and dropping to below 17fps when indoors/using a torch with no settings tweaks that can fix it.

It turns out the issue is actually with the engine version itself, which may be using incredibly outdated dependencies causing performance issues no matter the hardware.

## Fixing Performance

The performance fix in this guide is based on [this post](https://forums.rpgmakerweb.com/index.php?threads/how-to-update-nw-js-to-dramatically-improve-game-performance.131620/) which outlines how an important dependency to RPG Maker, `nw.js`, is incredibly outdated in the bundled version with the engine. While that guide discusses how to update the dependency in the engine itself for developers, you can also update it in the game files yourself.

1. Download the [latest stable](https://nwjs.io/downloads/) `SDK` version of `nw.js` (the normal version probably works too, the differences appear to be minimal)
1. Extract the files
1. Delete `swiftshaders` and `locales` from the game directory
1. Copy everything from the extracted files to the game directory
1. Delete the existing `Game.exe` and rename the `nw.exe` to `Game.exe`
1. You can try to execute the game now, but it might give you an error like `Required value ‘name’ is missing or invalid`. If this happens, open the `package.json` file in the root of the game directory and put something in the `name: ""` field.
1. At this point the game should now execute properly with better performance.
