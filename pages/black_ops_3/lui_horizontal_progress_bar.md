---
title: LUI Horizontal Progress Bar
keywords: blackops3, lui
last_updated: 1st January 2020
credits: [Blak, lilrifa, JariK]
summary: "A tutorial on creating a horizontal progress bar."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_horizontal_progress_bar.html
folder: black_ops_3
---

{% include note.html content="This guide covers how to do a traditional horizontal bar. If you want to do a circular progress bar, I recommend [lilrifa's tutorial on YouTube](https://youtu.be/Qt_QS_4HNxc)." %}

## Setting up the progress bar widget

To create a progress bar, simply create a `UIImage`. Then, apply one of these two materials: `uie_wipe` or `uie_wipe_normal`. These two materials differ in their 2d technique, `uie_wipe` "adds" color from the image whereas `uie_wipe_normal` will preserve the original image. You will also need to set shader vectors on this `UIImage`, which you can copy from the example below.

Here is an example progress bar widget:
```lua
local OverheatWeaponImage = LUI.UIImage.new(Elem, InstanceRef)
OverheatWeaponImage:setLeftRight(true, true, 15, -15)
OverheatWeaponImage:setTopBottom(true, true, 0, 0)
OverheatWeaponImage:setImage(RegisterImage("uie_t7_my_fancy_image"))

OverheatWeaponImage:setMaterial(RegisterMaterial("uie_wipe_normal")) --Set your choice of material here

--These following shader vector calls will configure it to work in the way we desire.
OverheatWeaponImage:setShaderVector(1, 0, 0, 0, 0)
OverheatWeaponImage:setShaderVector(2, 1, 0, 0, 0)
OverheatWeaponImage:setShaderVector(3, 0, 0, 0, 0)

Elem:addElement(OverheatWeaponImage)
Elem.weaponHeat = OverheatWeaponImage
```

## Updating the progress bar's percentage

Simply create a model subscription on whatever you want, and with the model value, do:
```lua
OverheatWeaponImage:setShaderVector(0, ModelVal, 0, 0, 0) --ModelVal should be in the range 0-1. If your model value is passing a percentage from 0-100, just divide it by 100.
```
Remember your nil check as normal. This is all you need for your progress bar to work. This was a shorter tutorial but it fleshes out the basics of using `setShaderVector`.