---
title: LUI Model Subscriptions
keywords: blackops3, lui
last_updated: 15th January 2020
credits: [Blak, Scobalula, JariK]
summary: "A guide on how to make use of models in LUI."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_subscribetomodel.html
folder: black_ops_3
---

## Overview
In LUI, you can connect to various game-based data via models. To do this, you select one for subscription, subscribe to it on a specific element, and can then set out a function to respond to any change.

There are multiple forms of model subscription - global subscriptions, normal subscriptions and element model subscriptions. All three of these will be covered in some form in this guide.

## Universal points
The principles of a model subscription as set out above are almost universal. Here are the key points to observe:
* The callback function will always pass the model reference as the only parameter.
* You can get the value of your model with `Engine.GetModelValue(ModelRef)`. 
* You must perform a nil check on your model value variable to ensure it is valid (by doing `if ModelVal then`). If a nil value is passed to a function such as `setText`, your game will UI Error.

## Element models
Element models are produced by a data source's models sub-table (see [Using UILists and Datasources](https://scobalula.github.io/wiki/black_ops_3/lui_uilists_datasources.html)), and can be accessed with the function `linkToElementModel`. Here is an example below:
```lua
--linkToElementModel(Parent, ModelName, RequiresSubscription(true), CallbackFunc)
BurgerText:linkToElementModel(Elem, "juicy", true, function(ModelRef)
    local ModelVal = Engine.GetModelValue(ModelRef)

    if ModelVal then
        BurgerText:setText(ModelVal)
    end
end)
```

With this, we've now linked `BurgerText` to the `juicy` property passed on from the data source, and have told the text to change based on what value is passed to it. This remains similar for other forms of model value, such as image names, etc, but they have their own quirks (like using `RegisterImage`).

## 'Normal' models
These models are the ones you will most often be working with. They are set out on the controller belonging to `InstanceRef`, and correspond for all manner of things, such as weapon ammo, grenades, et cetera.

Below is an example of a model subscription for weapon clip.
```lua
--subscribeToModel(Model, CallbackFunc)
MagazineText:subscribeToModel(Engine.GetModel(Engine.GetModelForController(InstanceRef), "CurrentWeapon.ammoInClip"), function(ModelRef)
    local ModelVal = Engine.GetModelValue(ModelRef)

    if ModelVal ~= nil then --Alternate way to nil check.
        MagazineText:setText(ModelVal)
        MagazineShadow:setText(ModelVal)
    end
end)
```
As you can see it's very similar to the element model subscription, the only real difference is the function to make the subscription.

### State model subscriptions
Due to the nature of states, the model subscriptions have a different callback so that they can trigger an update on the element state. Here is an example of a state-updating model subscription:

```lua
Elem:subscribeToModel(Engine.GetModel(Engine.GetModelForController(InstanceRef), "hudItems.playerSpawned"), function(ModelRef)
    --Here the parent element to the HUD is being told to trigger a state update on Elem, and will run the conditions set out in state conditions. See the Clips & States guide.
    HudRef:updateElementState(Elem, {name = "model_validation",
        menu = HudRef, modelValue = Engine.GetModelValue(ModelRef), 
        modelName = "hudItems.playerSpawned"})
end)
```

## Script notify
A script notify subscription can be setup to respond to a `LUINotifyEvent` from GSC. It has a few quirks which make it different. Here is an example script notify:
```lua
Elem:subscribeToGlobalModel(InstanceRef, "PerController", "scriptNotify", function(ModelRef)
    if IsParamModelEqualToString(ModelRef, "hello") then
        local NotifyData = CoD.GetScriptNotifyData(CoffeeRef)
        
        if NotifyData[1] == 1 then
            --Do something
        else
            --Do something else
        end
    end
end)
```

This notify would respond to the following GSC function: `player LUINotifyEvent(&"hello", 1, 1)`. This will be covered in greater detail in a dedicated script notify guide in future.
