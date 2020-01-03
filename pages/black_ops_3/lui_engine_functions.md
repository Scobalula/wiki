---
title: LUI Engine Function Reference
keywords: blackops3, lui
last_updated: 3rd January 2020
credits: [Blak, Scobalula, JariK, DTZxPorter]
summary: "This is a reference on various Engine functions."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_engine_functions.html
folder: black_ops_3
---

## List of LUI Engine functions

| Function | Arguments | Summary | Returns |
| -------- | ------- | -------- | ------- |
| CreateModel | (Object: Controller, String: Name) | Creates a model on the given controller. | (Object: ModelRef) |
| DvarBool | (Boolean: DefaultValue, String: DvarName) | Gets the value of a boolean dvar. Set arg1 to nil if you don't want a default value. | (Boolean: DvarValue) |
| DvarFloat | (Float: DefaultValue, String: DvarName) | Gets the value of a float dvar. Set arg1 to nil if you don't want a default value. | (Float: DvarValue) |
| DvarInt | (Integer: DefaultValue, String: DvarName) | Gets the value of an integer dvar. Set arg1 to nil if you don't want a default value. | (Integer: DvarValue) |
| DvarString | (String: DefaultValue, String: DvarName) | Gets the value of a string dvar. Set arg1 to nil if you don't want a default value. | (String: DvarValue) |
| Exec | (Instance?, String: Command) | Executes a console command. | Nothing |
| GetClientNum | (Object: Controller) | Gets the client number. | (Integer: ClientNum) |
| GetDvarType | (String: DvarName) | Gets the data type of the given dvar. | (DvarType) |
| GetGlobalModel | n/a | Gets the global model controller. | (Object: Controller) |
| GetModel | (Object: Controller, String: ModelName) | Gets the model on the given controller with a given name. | (Object: ModelRef) |
| GetModelForController | (Object: InstanceRef) | Gets a model controller. | (Object: Controller) |
| GetModelValue | (Object: ModelRef) | Gets the value of a given model. | (ModelVal) |
| HasPerk | (Unknown, String: PerkName) | Returns whether the player has a given perk. | (Boolean: HasPerk) |
| IsCampaignGame | n/a | Returns whether the current match is in Campaign. | (Boolean: IsCampaign) |
| IsCampaignGameZombies | n/a | Returns whether the current match is in Nightmares. | (Boolean: IsNightmares) |
| IsMenuLevel | n/a | Returns whether this is currently the lobby. | (Boolean: IsLobby) |
| IsMultiplayerGame | n/a | Returns whether the current match is in Multiplayer. | (Boolean: IsMultiplayer) |
| IsSplitscreen | n/a | Returns whether the user is on splitscreen. | (Boolean: IsSplitscreen) |
| IsUnlimitedAmmoWeapon | (String: WeaponName) | Returns whether the given weapon has unlimited ammo. | (Boolean: UnlimitedAmmo) |
| IsZombiesGame | n/a | Returns whether the current match is in Zombies. | (Boolean: IsZombies) |
| Localize | (String: UnlocalizedString) | Localizes the current string. | (String: LocalizedString) |
| LocalizeWithoutLocsMarkers | (String: UnlocalizedString) | Localizes the current string, without location markers around it being returned. | (String: LocalizedString) |
| SetDvar | (String: DvarName, Value) | Sets the value of a dvar. | Nothing |
| SetModelValue | (Object: ModelRef, Value) | Sets the value of a model. | Nothing |
| ToUpper | (String: Text) | Converts the string to all-uppercase. | (String: TEXT) |


## End note
I cannot guarantee that all the information here is 100% accurate however I've done my best. Feel free to make edits & corrections that you see fit.
