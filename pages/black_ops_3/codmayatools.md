---
title: CoDMayaTools
keywords: tool, plugin, patch, scripting, modding, black ops 3
last_updated: June 18th, 2020
credits: [Scobalula, Aidan, Maciej Zaremba, DTZxPorter (PyCoD), SE2Dev (PyCoD)]
summary: "A plug-in for exporting XAnims, XModels, and XCams from Maya"
sidebar: black_ops_3_sidebar
permalink: black_ops_3/codmayatools.html
folder: black_ops_3
---

Call of Duty Maya Tools supports exporting models, animations, and xcams from Maya. The tool allows modders to export existing assets from other games or custom assets into a Call of Duty standard file format.

This version includes fully working XModel/XAnim Bin files with notetracks, cosmetics, etc.

Supports:

* Models export as `.xmodel_export` or `.xmodel_bin`
* Animations export as `.xanim_export` or `.xanim_bin`
* Xcams export as `.xcam_export`

NOTE: This version has a lot stripped, as I would rather focus on the export functionality, if you want the old features, then you probably should use the older versions, I'm not supporting the other features.

### Installation

<div class="alert alert-success" role="alert"><i class="fa fa-download fa-lg"></i><a href="https://discord.gg/RyqyThu" target="_blank">Click Here</a> to join my Discord server to download the latest version.</div>

Simply drag and drop the files into your Maya's scripts folder in documents and add:

`python("import CoDMayaTools");`

to your usersetup.mel or use the one provided.

### Cosmetics

Unlike before, we can now mark specific joints as cosmetic, simply select the bones you wish to mark as cosmetic, and click the button to mark them.

If using the _cosmetic.mel file from Greyhound from Bo3/4, simply deselect everything, drag it on which will select all of the cosmetic bones the model uses, then click the button to mark them/

### Root Folders

To set your root folder, simply select the option to set it for the game you're working with, then tick the game you're working with in the settings menu