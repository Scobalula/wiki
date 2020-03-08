---
title: LUI Common Model Reference
keywords: blackops3, lui
last_updated: 8th March 2020
credits: [Blak, Scobalula, JariK, DTZxPorter]
summary: "This is a reference of various base UIModels available for use."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_model_reference.html
folder: black_ops_3
---

## List of common UIModels

*Scripted* models are ones that are not handled by the engine directly, and are not set up to behave as if they did. For these ones, you will probably need to add a `CreateModel` call to use them.

| Model Name | Data Type | Summary |
| -------- | ------- | ------- |
| CurrentWeapon.ammoInClip | Integer | Current weapon's magazine ammo |
| CurrentWeapon.ammoClipPercent | Float | Current weapon's magazine full percent |
| CurrentWeapon.clipMaxAmmo | Integer | Current weapon's maximum clip size |
| CurrentWeapon.ammoStock | Integer | Current weapon's reserve ammo |
| CurrentWeapon.weaponName | String | Current weapon's unlocalized display name |
| CurrentWeapon.equippedWeaponReference | String | Current weapon's code name (including mode suffix) |
| CurrentWeapon.weapon | Integer | A pointer of current equipped weapon for `Engine` functions |
| CurrentWeapon.ammoInDWClip | Integer | Current weapon's dual wield magazine ammo. A value of -1 indicates that there is no current dual wield weapon equipped. |
| CurrentPrimaryOffhand.primaryOffhand | String | Current lethal grenade slot icon |
| CurrentPrimaryOffhand.primaryOffhandCount | Integer | Current lethal grenade slot ammo count |
| CurrentSecondaryOffhand.secondaryOffhand | String | Current tactical grenade slot icon |
| CurrentSecondaryOffhand.secondaryOffhandCount | Integer | Current tactical grenade slot ammo count |
| CurrentWeapon.aat | String | *Scripted:* Current weapon's unlocalized AAT name |
| CurrentWeapon.aatIcon | String | *Scripted:* Current weapon's AAT icon |
| hudItems.playerSpawned | Boolean | Whether the player has spawned |
| zmhud.swordEnergy | Float | Percentage charge on the player's specialist weapon |
| zmhud.swordState | Integer | Current state of specialist weapon. Check the `_zm_hero_weapon` script for what these mean. |
| hudItems.showDpadDown | Boolean | Whether to show the bottom dpad slot (Action Slot 2/Shield) |
| hudItems.showDpadUp | Boolean | Whether to show the top dpad slot (Action Slot 1/GobbleGum) |
| hudItems.showDpadRight | Boolean | Whether to show the right dpad slot (Action Slot 3/Mines) |
| hudItems.showDpadLeft | Boolean | Whether to show the left dpad slot (Action Slot 4/Alt Weapon) |
| hudItems.doublePointsActive | Boolean | Whether Double Points is currently active |
| hudItems.pulseNoAmmo | Boolean | Whether to produce the "pulse" effect when a player tries fire without ammo |
| bgb_display | Boolean | Whether to display a GobbleGum |
| bgb_timer | Float | Percentage time left on a GobbleGum |

## End note
I cannot guarantee that all the information here is 100% accurate however I've done my best. Feel free to make edits, additions & corrections that you see fit.
