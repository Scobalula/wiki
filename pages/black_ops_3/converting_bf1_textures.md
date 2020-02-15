---
title: 
keywords: blackops3, battlefield1, assets
last_updated: 15th February 2020
credits: [Blak, Scobalula, DamianoTBM]
summary: "A tutorial on how to convert Frosty-ripped Battlefield 1 textures to the Black Ops III workflow."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/converting_bf1_textures.html
folder: black_ops_3
---

{% include important.html content="It is highly recommended to download and use [CoDImageTool](https://github.com/Scobalula/CoDImageUtil) for sections of this guide (you won't be guided on how to do things the hard way if CoDImageTool has an easy way). You will also need [Frosty Editor](https://frostytoolsuite.com/downloads.html) for ripping textures from Battlefield 1 (this will not be covered in the scope of this guide however)." %}

## Overview
In Battlefield 1, weapon textures are stored within two images; a `NRM` texture and a `CS` texture. The overall workflow for BF1 guns is: Color, Normal, Metallic, Gloss. Obtaining & where necessary converting these textures will be covered in this guide.

## Obtaining Gloss
In CoDImageTool, select the Mode `Split RGB/A (Spec/Gloss, etc.)`. With this selected, drop your `CS` texture onto the tool. It will split it into two textures, suffixed `_g` and `_s` respectively.

Here, the gloss map is the `_g` texture. This is already compatible with Black Ops III.

![Gloss map](https://i.gyazo.com/710052405d82899b1c9410b83e5c374a.png)

## Obtaining Specular & Color (Diffuse)

### Obtaining the BF1 color map & metallic mask
Assuming you have done the above, you should have an `_s` texture for your `CS`. This is your BF1 color map.

Now, in order to convert the workflow, you need to run Mode `Split RGB/A (Spec/Gloss, etc.)` on the `NRM` texture too. It will, like the `CS`, produce two textures: `_g` and `_s`. Here your metallic mask is the `_g` map.

### Converting the BF1 color map to Specular & Diffuse
With this, you now need to rename your `NRM_g` texture to be the same name as the BF1 color map plus `_mask`. Select Mode `Split Specular Color` in CoDImageTool, and then drag your BF1 color map into it. It will produce two images, suffixed `_c` and `_s`. `_c` is your diffuse map, and `_s` is your specular map for use in Black Ops III.

![Diffuse map](https://i.gyazo.com/c9fe2f97ab9d6fa51bedc12759478be4.png)
![Specular map](https://i.gyazo.com/614b02b88df1dcc57f24c2adf2e8c474.png)

## Obtaining Normal
### Step 1
Above you've split the `NRM` into two textures. The texture we are working from now is the `_s` texture.

Open the `_s` texture in your chosen image editor, and decompose the RGB channels into three greyscale layers. You need to invert the color of the 2nd / GREEN channel.

### Step 2
Recompose the channels back into RGB and export your image.

Now, set your CoDImageUtil Mode to `Patch Yellow Normal Map (XY)`, and drag in your image. It will convert it from a yellowscale normal map to bluescale, which you can now use in Black Ops III.

![Normal map](https://i.gyazo.com/2b9fe88841f5830512cb1fc3f7e0d29e.png)

## Obtaining Ambient Occlusion
In CoDImageTool, select Mode `Split All Channels`. Go back to your initial `NRM` texture and drag this into the tool. It will produce four images (`_a`, `_b`, `_g` and `_r`). The texture suffixed `_b` is your ambient occlusion map, which you can use out of the box with Black Ops III.

![Occlusion map](https://i.gyazo.com/92cb676d17e360e5a3a7cd24993b3ec6.png)

## Final notes
Beware that Battlefield 1 often uses tinting on parts of the gun (i.e. on wooden sections), which you will need to manually edit yourself on your `CS_s` image.

The gloss range you use may depend on what you personally prefer and on the gun, but a baseline you could try is `1-11`, which I used on the Nagant revolver and that turned out quite nicely.

![Nagant revolver](https://i.gyazo.com/201feb8c1336c4e881f07a443e23cd43.jpg)