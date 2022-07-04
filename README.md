# This is a modified and debloated .appx for the 1.16.40.02 version of Minecraft for Windows
## Made by ambient, with help from r4isen1920 and AgentMindstorm for the Marketplace and Realms Plus UI removal 


### Disclaimer:
- obtaining a copy of a Minecraft for Windows app package (.appx) will **NOT** allow you to pirate the game. you **MUST** still own the game in order for it to be played outside of trial mode (identical behavior to Minecraft for Windows appxs downloaded directly from the Microsoft Store)


### Feature List:
- 1.14.60 loading screen logo (now HD) & white background
- removed all Marketplace, Realms Plus advertisements, and unnecessary buttons in UI (see the *_global_variables.json* header for more details)
- removed the 1.16+ background shadow in hud tooltip and title texts, and added back the text drop shadow as a replacement (like 1.14.60)
- ported over the 1.14.60 server selection screen to the latest version (more performant, less cluttered)
- included built-in [1.7 animations](https://mcpedl.com/java-1-7-animations/) for 1.16.0-1.16.40, with official cape support (redder armor, no extra particles subpack)
- removed ~75mb worth of bloat by compressing aquatic and nether update music files (thanks [notshige](https://github.com/NotShige)), as well as deleting the unused HTML UI assets
- disable sending certain telemetry to Microsoft servers
- disable realms services (since they are deprecated in versions that don't have the latest protocol versions)
- optionally choose a patched binary to enable the 1.12.1 skin picker screen and fully disable persona and emote bloat
  
#### Other Minor QOL Fixes
- fixed [MCPE-103016](https://bugs.mojang.com/browse/MCPE-103016), [MCPE-46975](https://bugs.mojang.com/browse/MCPE-46975), and [MCPE-51982](https://bugs.mojang.com/browse/MCPE-51982)
- removed the liquid offset when the camera is inside a liquid
- removed the report button in the player list
- prevented container screens from closing when the player takes damage



### Download Summary
- `Minecraft-1.16.40.02_debloated_legacy.appx` - (**RECOMMENDED**) includes the legacy skin picker patch, uses the 1.12.1 skin picker screen, disables emotes entirely
- `Minecraft-1.16.40.02_debloated.appx` - does NOT include the legacy skin picker patch, uses the vanilla persona character creator screen
- `skin_pack_loading_fix.mcpack` - skin pack to fix infinitely loading skins when installing custom capes. this is recommended if you are using custom capes
- `ui_debloater_1.16.40.mcpack` - standalone version of the UI modifications in this appx. only for people who just want UI changes and don't want to install a new appx. the contents of this pack are already built into both appxs
- `custom_cape_templates.zip` - includes the `persona` and `vanilla` folders, respectively, for custom cape installation


### Installation
- these app packages are considered "untrusted" by Windows, because they were packaged by a 3rd party (me)
- in order to install the appx's certificate, right click it, and go `Propeties` -> `Digital Signatures`
- click the signature in the signatures list, the click `Details` -> `View Certificate` -> `Install Certificate...`
- select the `Store Location` to be `Local Machine`, then click `Next`
- select `Place all certificates in the following store` and set the directory to the `Trusted Root Certification Authorities` folder
- click `Next`, then `Finish`
- double click the appx to install with the default App Installer
- note: if you do not trust these steps, feel free to unzip the appx into a folder and repackage it yourself with the tool below, or install in extracted format with powershell



### _global_variables.json
- this file can be found in `.\data\resource_packs\vanilla_1.16\ui\_global_variables.json` and can be edited accordingly
- changes to this file will only apply after a restart of Minecraft
```
{
  // toggles the "persona" customization tab. existing persona skins will not be affected but cannot be edited for as long as this is disabled
  "$enable_persona_customizations": false,
  
  // allow "buy" or "purchase" buttons to be rendered or not in the *profile* customization screen only. if disabled, everything unpurchased will be marked as locked and cannot be purchased until it is re-enabled
  "$enable_purchase_buttons": false,

  // renders all custom skin packs in the legacy skin picker screen
  // only valid if you are using the 1.16.40 binary patch to enable the legacy skin picker UI
  // setting this to false will make locked AND unlocked skin packs inaccessible, unfortunately there is no way to distinguish between the two with JSON UI
  // if set to false, custom capes must be added by modifying the ".\data\skin_packs\vanilla\" folder
  "$enable_legacy_skin_picker_custom_skin_packs": false,

  // adds the achievements button to the start screen, similar to versions 1.12.1 and older
  // if you are using the 1.16.40 binary patch to enable the legacy skin picker UI, keep this set to false since the patch automatically adds this button in the start screen for some reason
  "$enable_start_screen_achievements_button": false
}
```


### About Custom Capes
- custom capes are not included in the appx by default (because not everyone wants them), so you must install the template manually
- there are 2 different .appxs on the releases page. one includes the binary patch to enable the legacy skin picker (cleaner UI, more performant, at the cost of disabling persona and not being able to equip/swap/view emotes as stated above)
	- if you are using the release with the *persona character creator* enabled, you may change your skin and cape texture by navigating to `.\data\skin_packs\` and replacing the `persona` folder in the appx with the `persona` folder from the in the `custom_cape_templates.zip` on the releases page. you can change the cape and skin textures in there accordingly, or add more skin entries. this method is identical to the [BionicBen custom capes method](https://www.youtube.com/watch?v=spJRWCe5Vy0), which goes into greater detail about the process
	- if you are using the release with the *legacy skin picker* enabled, the process is *the exact same*, except you need to replace the `vanilla` folder instead of the `persona` folder, and you are only limited to replacing the steve and alex skins. however, if you set the `$enable_legacy_skin_picker_custom_skin_packs` in `.\data\resource_packs\vanilla_1.16\ui\_global_variables.json` to `true` (set to false by default), the process would then be the same as if you are using the appx with the persona creator still enabled.



### Packaging Tools Used
- [WSAppBak](https://github.com/Wapitiii/WSAppBak)