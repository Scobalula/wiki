---
title: "Call of Duty: MWR MP Characters"
keywords: assets, characters, download, zombies
last_updated: June 25th, 2020
credits: [Scobalula, DTZxPorter, Activision/Infinity Ward, ThomasCat for T7 -> T7 rig]
summary: "This tutorial will show you how to install the Call of Duty: MWR MP Characters into your zombies map."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/mwr_mp_characters.html
folder: black_ops_3
---

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://discord.gg/RyqyThu" target="_blank">Click Here</a> to join my Discord server to download the latest version by searching in: 📦scob-releases A7646A68 once you have joined.</div>

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://imgur.com/a/jDMzKH1" target="_blank">Click Here</a> to view screenshots of the MWR MP Characters</div>

{% include important.html content="This tutorial does not include a customization table and uses a simple XModel override, if you don't know what a customization table is you probably don't need one, if you do and need one, you'll need to set up it up yourself." %}

{% include important.html content="If you get duplicate erros, do not report them to me, fix them yourself, duplicate errors are almost never an issue with an asset package you download unless stated otherwise, and usually it's 100% fixable by yourself if you use that thing between your shoulders. **NEVER TICK IGNORE ERRORS FOR DUPLICATE ERRORS.**" %}

To start simply copy over the folders, excluding the `do_not_copy_this_folder_see_readme` folder, to your Call of Duty: Black Ops III folder.

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

Next you'll want to go over to `Call of Duty Black Ops III\zone_source\all\assetlist` and open the file `core_common.csv` in any text editor, this is simply one of the files linker will read to determine assets it should ignore, we don't want it to ignore our characters, so we'll want to remove the above lines from this file, either by removing the lines by deleting them, or by adding `// ` to the start of each line to comment them out.

Next we'll need to determine which set of characters we'll want to add to our map, go to the folder `do_not_copy_this_folder_see_readme\options` in the included download and you'll se a folder for each faction and a mixed folder (which is simply one guy from the SAS, Spetnaz, Opfor, and USMC faction), these each contain a version of the xmodel override GDT that is set up for that case, depending on which one you want to install, you'll need to go into the folder of the one you want to add to your map and copy over the source_data folder to your Bo3 folder. In the future you can easily swap out this gdt with each of them, as it is the same gdt used across my releases. If you want and know how, you can also use a customization_table for more control, but again that is not covered in this tutorial.

Once done you can simply link your map and you should have working MWR Characters, if you run into issues, fully check the log, as these were ported over 2 years ago, I'll only accept issue reports with the installation or game breaking issues (i.e. missing assets), please do not report quirks, etc. with them.