---
title: Setting up Weapon Attachments
keywords: blackops3, weapons
last_updated: 1st January 2020
credits: [Blak, Scobalula, DTZxPorter, JariK, Marvel4]
summary: "A guide on how to setup attachments on your weapon port."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/setting_up_weapon_attachments.html
folder: black_ops_3
---

## Introduction
Black Ops III (and Black Ops II) use a setup for attachments which allows users to apply attachments with the console (weaponname+attachment+attachment…) and customize weapons to have attachments (either levelcommon or weapon kits), without the need for additional weaponfiles. This tutorial intends to document this setup and guide users to give their weapon ports this capability. It’s not recommended to use this in a standalone map unless you plan on configuring weapon kits, as you will likely have a set idea of what you will use on your gun and can set it up in your weaponfile.

{% include note.html content="This tutorial will cover the T7-T7 process of setting up weapon attachments, however various aspects of it will be similar for other games." %}

## Prerequisite
Before starting the tutorial, you need [HydraX](https://github.com/Scobalula/HydraX) - This is for getting the weaponfiles of your Black Ops III weapons, the attachment uniques, etc, as Black Ops III's attachment model offsets are applied in APE. As Porter's weapon info dump doesn't appear to be available anymore, you will need HydraX for the offsets even if you plan on making the AUs yourself.

With HydraX, get the following:
* Your weapon's weaponfile
* Your weapon's attachment unique assets `au_weaponname_...`

It is also recommended to have a good level of Maya and APE knowledge. If this is one of your first ports in general you should come back to this tutorial when you are more experienced.

# Maya

## Setting up the skeleton and animations to work with attachments
When creating the skeleton for your weapon (also known as the animated model - or animmodel), you need to include all animated attachments rigged to the weapon with the correct joints. These include but are not limited to: Extended Mags, Fast Mags and Rapid Fire. Some weapons animate more attachments (such as the KVK 99m, which animates its Long Barrel). Beware of this.

{% include note.html content="As a general rule of thumb, you can rely on attachments with suffix `_animate` on their joints to suggest that they need to be on your skeleton. **Beware however that there are exceptions, and some attachments animate without this suffix.**" %}

Your attachments need to be correctly offsetted on your skeleton. You can obtain these offsets from the attachment unique assets you ripped with HydraX. Open these assets in APE, find the **Attachment #X** sections, and for each model listed under them, find Offset and/or Angles and convert these to **cm** (Maya works in **cm**, APE works in **inches**.). Then apply these offsets in Maya in your skeleton's scene.

The reason you have to do this process is because the skeleton needs to know what to animate - and if there are joints missing when an animation is imported they will not be animated. Once you have setup your skeleton correctly, port over all of your animations like you would with any weapon.

# Into the mod tools

## Attachment assets
*Not to be confused with Attachment Unique assets.*

Treyarch provided us with some, but not a massive amount of the attachment assets in the Mod Tools. You can find what they provided in the `weaponattachments` GDT.

### Missing attachments
Treyarch did not provide us most notably the attachments `ir` and `damage`. This is because they only gave us the attachments used on the Kuda. Rip these with HydraX and add them yourself.

Additionally, they did not provide us many special case attachments, such as Pack a Punch, and per-weapon ones. You will also need to get these with HydraX and add them in.

### What attachments does my weapon need?
Refer to the stringtable `attachmentmappingstable.csv` (found at `share/raw/gamedata/weapons/common/attachmentmappingsTable.csv`). In there is every Black Ops III weapon's attachment setup that Treyarch gave. Find the entry for your weapon, and there you can see what attachments you need for your weapon.

{% include note.html content="You will need to create more entries in this file if you're doing weapons from other games and/or if your weapon is a Black Ops III DLC weapon that does not have an upgraded entry. As this file was given to us in the tools, it will be reset if your verify files or the tools are updated, so create a local copy in your map or mod's folder, at `FOLDER/gamedata/weapons/common/attachmentmappingsTable.csv`. Edit it as required." %}

### What is the purpose of an attachment asset?
Attachment assets set up the generalised properties for a specific attachment, such as magazine size multipliers, rate of fire multipliers, etc. So for example, if you had the CoD WW2 PPSh-41, and wanted it to get a 71 mag on Extended Mags from 35, you would need to create a dedicated attachment asset for it (naming it something like `extclip_s2_ppsh`) and changing the multiplier for mag size. You would then need modify your attachment mappings table to load this attachment for your PPSh.

### Weapon port etiquette
It's important to remember that if you are keeping any additional attachment assets under `weaponattachments`, if you are releasing these ports, you could then cause interference if multiple people release ports, all using `weaponattachments`. Instead, for the sake of compatibility, Cut your attachments and put them under a GDT that will not interfere.

### Troubleshooting
#### One of the attachments on my weapon is not applying in-game**
This attachment is using an attachment asset which you do not have in your mod tools. Check the attachment mappings table to see what attachment it is, rip it with HydraX and add it to your APE. It's not necessary to put it into your zone.

#### Linker is erroring, saying `attachment_name` not found**
Again, you do not have your attachment in your mod tools, and it wasn't provided to us in the asset lists either (this is why it's outright errored). Follow the same process above to acquire it.

## Attachment Unique assets
Attachment Unique assets do what their name suggests, they specify the unique features of a gun’s attachment. Treyarch use these to change animations, apply xmodels, hide tags or set other unique features that would not be able to be generalized with an attachment asset.

### Structure
*Information: This part of the tutorial has been repurposed to be for porting from games other than Black Ops III, as everything is now accessible via HydraX and it's simply impractical to do your attachment uniques manually now.*

Attachment Uniques on a weapon are structured with a base attachment (suffixed `_none`), with all other attachments organised below it.

### Setting up an attachment unique asset
Create an `attachmentUnique` asset in your GDT. A rule of thumb of what to call it is `au_weaponname_none`, however other naming schemes are possible with Attachment Unique Base (see Pack a Punched Version).

From here, you can derive each of your weapon’s attachments under `_none`, giving them suffixes like `_extclip`, `_fastreload` among others. In the assets, you set any models needed under `Attachment #X`, under View & World models. Changes in animations are applied under `XAnims`. If your weapon needs certain parts hidden when an attachment is applied, use the field `Hide Tags` for this.

{% include important.html content="You need to specify in your AU assets the `attachmenttype` and `Attachment Association`. What you set these to is self-explanatory." %}

{% include note.html content="Many games use a `tag_sight_off` and `tag_sight_on` system (or similarly named) where off is hidden when the player is using iron sights and on is hidden when the player is using an optic. Ensure that you put `tag_sight_off` (or however it is named for the gun) in your root Attachment Unique asset and change it accordingly to its on counterpart for any optic Attachment Unique asset." %}

### What about attachments that have combined behaviour?
Such examples of this would be Fast Mags + Extended Mags, etc. For this, derive under one of the two attachments, and name it `attachment1+attachment2`. The `attachmenttype` becomes the second attachment, then if you now have multiple models, for example your `Attachment #2` might instead have `Attachment Association` for the second attachment. Once again, you can change animations if necessary under `XAnims`.

## Specific attachment cases
Some attachment unique assets are much less plug and play to setup. This subheading will provide information for those in question.

### Extended Mags, Fast Mags or both
For Extended Mags or Fast Mags, you can setup the Attachment 1 model as normal (and its offsets will likely be identical to the base magazine model). However, there is one extra attribute to check: `Disable Weapon Clip Attachment` This tells the game to disable the base magazine attachment set in the weaponfile (meaning that for your base gun, the magazine should be a separate model).

When handling both (which is normally derived from `extclip` as `extclip+fastreload`, you might need to specify a fast mags attachment as Attachment 2 or use `ext_fast_mag` (Black Ops III) as Attachment 1. This depends on the weapon. You also generally need to specify the Fast Mag (Reload Quick) reload animations, however it is possible certain weapons have dedicated extended fast mag reloads.

### Varix 3 (dualoptic) and/or Hybrid Optics
Varix 3’s Attachment Unique asset is setup like any other attachment except that you need to specify an Alt Weapon Name (`dualoptic_weaponname`).

{% include important.html content="Never use a weapon’s mode suffix when specifying an Alt Weapon Name (these suffixes being `_zm`, `_mp`, or `_cp`)." %}

Ensure, still within the Attachment Unique asset, that the following animations are specified:
```
ADS Up - yourweapon_ads_hybrid_upper_up
ADS Down - yourweapon_ads_hybrid_upper_down
ADS Up - Other Scope - yourweapon_ads_hybrid_lower_up
```

Now that you have completed the part within the Attachment Unique asset, you now need to derive your weapon’s weaponfile and name it `dualoptic_YOURWEAPONNAMEHERE`.

{% include note.html content="Ensure that within your non-dualoptic weaponfile that `Alt Weapon Name` is not specified, and `Ads Only Alt Weapon` and `Disable Toggle Weapon Switching` are checked. These can be found under `Alt Mode Options`." %}

Within your `dualoptic_` weaponfile, you need to specify `Alt Weapon Name` as your original weaponfile’s name and make sure your dualoptic weapon has these fields setup:
```
Inventory -> altmode
ADS Up -> yourweapon_ads_hybrid_upper_up
ADS Down -> yourweapon_ads_hybrid_lower_down
ADS Up - Other Scope -> yourweapon_ads_hybrid_lower_up
```

Make sure to include the dualoptic weaponfile in your zone file (`weaponfull,dualoptic_WEAPONNAME`).

### "Special Combo" - Extended Mags, Fast Mags and Grip
For this case, there are no extra Attachment Unique assets needed. Simply, within your weaponfile, specify your weapon’s equivalent of the following animations:
```
Reload Special Combo -> yourweapon_grip_reload_dm
Reload Special Combo Empty Anim -> yourweapon_grip_reload_empty_dm
Reload Special Combo Quick -> yourweapon_grip_reload_dm_quick
Reload Special Combo Quick Empty -> yourweapon_grip_reload_empty_dm_quick
```

### Suppressor (suppressed)
Set up your suppressor fire sounds in `Sounds` in your attachment unique asset.

### Ignore if not using Loop or Burst Sounds: Suppressor and Rapid Fire
Like "Special Combo", there's no need for an extra attachment unique asset. Find the fields `Suppressed Rapid Fire Loop/Burst Fire` in the `Sounds` section of your weaponfile, and edit those accordingly.

## Pack a Punched Version
In order to get your Pack a Punched weapon to load in attachments, you will need to set its `Attachment Unique Base`. This is found within the weaponfile, under `Misc`. To set this, you need to omit the suffix of your base Attachment Unique asset. For example, if the base Attachment Unique asset is `au_ar_an94_none`, you should put `au_ar_an94` as your `Attachment Unique Base`.

## Zone file
When putting your weapon into your zone file, you need to specify `weaponfull` instead of `weapon`. This tells Black Ops III to load in your weapon’s attachments (and cosmetics if you put those in too).

Linker should convert the attachments if you have setup everything else correctly.

## Specifying to Black Ops III what attachments to load on your weapon
Find your `attachmentmappingsTable.csv` under `share/raw/gamedata/weapons/common`. Open it.

Do not be alarmed. This file is actually quite simple, you merely have to specify the weapon name as the first parameter, and list all attachment assets it uses as the second parameter, each divided by a space.

Copy a line that is somewhat similar to your weapon’s and adjust it to how you need it.

Example: `ar_charlton_s2,reflex_s2 acog quickdraw fmj extbarrel_ar rf grip damage steadyaim_s2 supply`

You will also need to do a line for your weapon’s upgraded version - and a line for dualoptic is not required.

{% include note.html content="All Black Ops III customizable weapons are already provided in this file, but you will need to create a line for their Pack a Punched version if they were not featured in Zombies" %}

# Finished
This is all you need to setup your weapon with attachments. You should have a coffee to celebrate.