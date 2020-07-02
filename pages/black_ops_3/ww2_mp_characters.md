---
title: "Call of Duty: World War II MP Characters"
keywords: assets, characters, download, zombies
last_updated: June 25th, 2020
credits: [Scobalula, DTZxPorter, Activision/Sledgehammer Games, ThomasCat for T7 -> T7 rig]
summary: "This tutorial will show you how to install the Call of Duty: World War II MP Characters w/ Primis Heads into your zombies map."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/ww2_mp_characters.html
folder: black_ops_3
---

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://discord.gg/RyqyThu" target="_blank">Click Here</a> to join my Discord server to download the latest version by searching in: 📦scob-releases 0A8C32AA once you have joined.</div>

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://imgur.com/a/2zzLqLd" target="_blank">Click Here</a> to view screenshots of the WW2 MP Characters</div>

{% include important.html content="This tutorial does not include a customization table and uses a simple XModel override, if you don't know what a customization table is you probably don't need one, if you do and need one, you'll need to set up it up yourself." %}

{% include important.html content="This tutorial does not include a customization table and uses a simple XModel override, if you don't know what a customization table is you probably don't need one, if you do and need one, you'll need to set up it up yourself." %}

{% include important.html content="snd_convert has a few bugs including randomly throwing exceptions for valid audio files, so with that in mind, it may be required to compile a few times if you get object reference/missing source checksum errors for sounds to work." %}

To start simply copy over the folders, excluding the screenshots folder, to your Call of Duty: Black Ops III folder.

Next open your map's zone file, this can be done by right clicking your map in Launcher and clicking "Edit Zone File" which will open it in a text editor, or by going to your map's folder and opening the .zone file.

Once opened, you'll want to add the following to it, adding it to the bottom will be fine to make things easy:

```
xmodel,c_zom_der_dempsey_mpc_fb
xmodel,c_zom_der_dempsey_viewbody
xmodel,c_zom_der_dempsey_viewhands
xmodel,c_zom_der_dempsey_viewlegs
xmodel,c_zom_der_nikolai_mpc_fb
xmodel,c_zom_der_nikolai_viewbody
xmodel,c_zom_der_nikolai_viewhands
xmodel,c_zom_der_nikolai_viewlegs
xmodel,c_zom_der_richtofen_mpc_fb
xmodel,c_zom_der_richtofen_viewbody
xmodel,c_zom_der_richtofen_viewhands
xmodel,c_zom_der_richtofen_viewlegs
xmodel,c_zom_der_takeo_mpc_fb
xmodel,c_zom_der_takeo_viewbody
xmodel,c_zom_der_takeo_viewhands
xmodel,c_zom_der_takeo_viewlegs
image,uie_t7_zm_hud_score_char1
image,uie_t7_zm_hud_score_char2
image,uie_t7_zm_hud_score_char3
image,uie_t7_zm_hud_score_char4
```

Next you'll want to go over to `Call of Duty Black Ops III\zone_source\all\assetlist` and open the file `core_common.csv` in any text editor, this is simply one of the files linker will read to determine assets it should ignore, we don't want it to ignore our characters, so we'll want to remove the above xmodel/image lines from this file, either by removing the lines by deleting them, or by adding `// ` to the start of each line to comment them out.

Next we'll add the voice lines, for this you'll need to go over to your scz file located in the `sound/zone_config` in folder in your map's folder. Once open add the following to the Sources array:

```json
{
  "Type" : "ALIAS",
  "Name" : "zm_giant_vox",
  "Filename" : "zm_giant_vox.csv",
  "Specs" : [ ]
},
```

Make sure to match the format and syntax of this file, if possible, use a text editor with JSON highlighting. I recommend VS Code as it can show errors clearly.

Next open your map's gsc file located in the `scripts/zm folder` of your map's folder. Once open add the following to the main function, adding to the end is fine, above the }:

```cpp
level thread custom_add_vox();
```

Then add the following function to your gsc file, adding to the end of the entire file is fine:

```cpp
function custom_add_vox()
{
	zm_audio::loadPlayerVoiceCategories("gamedata/audio/zm/zm_giant_vox.csv");
}
```

Once done you can simply link your map and you should have working Space Suits, if you run into issues, fully check the log, these have been tested and work, so any issues are more than likely on your end.