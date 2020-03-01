---
title: Enabling left DPAD HUD
keywords: blackops3, lui
last_updated: 1st March 2020
credits: [Blak, Scobalula, xSanchez78]
summary: "A guide on how to enable the left DPAD HUD in LUI."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_enabling_left_dpad.html
folder: black_ops_3
---

{% include important.html content="This guide will not cover how to do the functionality for the UIModels on the GSC side to use the Left DPAD. You can export the logic from Moon/Origins's scripts using [Cerberus](https://github.com/Scobalula/Cerberus-Repo/releases). The Wave Gun's UIModel logic is stored within its dedicated weapon script. The Staff UIModel logic is stored in the `zm_tomb_utility` script." %}

{% include note.html content="You will need a `t7hud_zm_mapname` LUI setup for your map to follow this guide, however this is an expectation for all LUI guides on this wiki..." %}

## Editing the Ammo HUD to enable the left DPAD
Find `AmmoWidget:setTopBottom(false, true, -232.000000, 0.000000)` in your `t7hud_zm_mapname` file. Below this, add the following:

```lua
    -- Change wave gun's icons
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadIconWaveGun.IconImgMineDisabled:setImage(RegisterImage("uie_t7_zm_hud_ammo_icon_wavegun"))
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadIconWaveGun.IconImgMineActive:setImage(RegisterImage("uie_t7_zm_hud_ammo_icon_wavegun_active"))
    
    -- Change staff's icons
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadIconStaff.IconImgMineDisabled:setImage(RegisterImage("uie_t7_zm_hd_hud_ammo_icon_staff_inactive"))
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadIconStaff.IconImgMineActive:setImage(RegisterImage("uie_t7_zm_hd_hud_ammo_icon_staff_active"))
    
    -- Show ldpad ammo
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadAmmoNumbersLeft:mergeStateConditions({
        {
            stateName = "Visible",
            condition = function(Hud, Element, StateTable)
                return AlwaysTrue()
            end
        }
    })
    
    -- Cover the fuse on the hud
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadLeftCover:mergeStateConditions({
        {
            stateName = "On",
            condition = function(Hud, Element, StateTable)
                return AlwaysTrue()
            end
        }
    })
    
    -- Show the background box on the ldpad ammo
    AmmoWidget.ZmAmmo.ZmAmmoProp0.DpadIconCounter:mergeStateConditions({
        {
            stateName = "On",
            condition = function(Hud, Element, StateTable)
                return AlwaysTrue()
            end
        }
    })
    
    -- Adjust clip info to fit with the ldpad
    AmmoWidget.ZmAmmo.ZmAmmoClipInfo0:mergeStateConditions({
        {
            stateName = "WeaponDualOffsetLeft",
            condition = function(Hud, Element, StateTable)
                return IsModelValueGreaterThanOrEqualTo(arg1, "currentWeapon.ammoInDWClip", 0.000000)
            end
        },
        {
            stateName = "WeaponOffsetLeft",
            condition = function(Hud, Element, StateTable)
                return AlwaysTrue()
            end
        },
        {
            stateName = "Weapon",
            condition = function(Hud, Element, StateTable)
                return AlwaysFalse()
            end
        },
        {
            stateName = "WeaponDual",
            condition = function(Hud, Element, StateTable)
                return AlwaysFalse()
            end
        }
    })

```

You can see what everything is doing here, just follow the comments above each block of code.

What we've done here is overrode all of the state conditions that were checking for Origins & Moon specifically, so that the left DPAD will be enabled on all maps. It's now up to you to setup code to handle the UIModels that these widgets use.

## Extra notes
At the top of the code are function calls to change the icons for the wave gun & staff. The easiest way to do your alt weapons (assuming you're not doing Staff/Wave Gun) is to just change these images and use the UIModels associated with them to save time.

Attached below are the clientfield register calls for the UIModels that the Left DPAD uses:

GSC
```
clientfield::register( "clientuimodel", "hudItems.showDpadLeft_Staff", VERSION_TU21, 1, "int" );
clientfield::register( "clientuimodel", "hudItems.showDpadLeft_WaveGun", VERSION_TU21, 1, "int" );
clientfield::register( "clientuimodel", "hudItems.dpadLeftAmmo", VERSION_TU21, 2, "int" );
```

CSC
```
clientfield::register( "clientuimodel", "hudItems.showDpadLeft_Staff", VERSION_TU21, 1, "int", undefined, !CF_HOST_ONLY, !CF_CALLBACK_ZERO_ON_NEW_ENT );
clientfield::register( "clientuimodel", "hudItems.showDpadLeft_WaveGun", VERSION_TU21, 1, "int", undefined, !CF_HOST_ONLY, !CF_CALLBACK_ZERO_ON_NEW_ENT );
clientfield::register( "clientuimodel", "hudItems.dpadLeftAmmo", VERSION_TU21, 2, "int", undefined, !CF_HOST_ONLY, !CF_CALLBACK_ZERO_ON_NEW_ENT );
```