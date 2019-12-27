---
title: LUI Element Function Reference
keywords: blackops3, lui
last_updated: 27th December 2019
credits: [Blak, Scobalula, JariK, DTZxPorter]
summary: "This is a reference with examples on how to use various LUI element functions."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_element_functions.html
folder: black_ops_3
---

## List of LUI element functions

{% include note.html content="These functions have been obtained from luielement.lua which was ripped with Greyhound. These are the majority of the functions found in there, but some have been kept out either because they are not understood or they are redundant as other functions here cover them." %}

{% include note.html content="Function summaries marked with an asterix have examples of use further down. *Italic* arguments are optional." %}

| Function | Arguments | Summary | Returns |
| -------- | ------- | -------- | ------- |
| addElement | (UIElement: Element) | *Adds the specified element as a child. | Nothing |
| addElementBefore | (UIElement: Element, UIElement: ElementAfter) | Adds the specified element as a child, before the other specified element. | Nothing |
| addElementAfter | (UIElement: Element, UIElement: ElementBefore) | Adds the specified element as a child, after the other specified element. | Nothing |
| canAddElement | (UIElement: Element) | Checks whether the specified element can be added. | Boolean: (true = Yes, false = No) |
| unsubscribeFromAllModels | n/a | Removes all element subscriptions. | Nothing |
| setModel | (Object: Model) | Sets a model on this element | Nothing |
| linkToElementModel | (UIElement: Element, String: Model, Boolean: RequiresSubscription, Function: Callback(Object: ModelRef)) | *Subscribes to a model specific to the element | Nothing |
| subscribeToElementModel | (UIElement: Element, String: Model, Function: Callback) | Subscribes to a model specific to the element. Calls linkToElementModel with RequiresSubscription set to true. | Nothing |
| subscribeToGlobalModel | (Object: InstanceRef, String: Scope, String: Model, Function: Callback(Object: ModelRef)) | *Subscribes to a global model. | Nothing |
| unsubscribeFromGlobalModels | n/a | Unbinds the element from all of its global model subscriptions. | Nothing |
| isClosed | n/a | Determines whether an element has been closed. | Boolean: (true = Yes, false = No) |
| close | n/a | *Closes the element it is called on. | Nothing |
| closeAndRefocus | (UIElement: Element) | Closes the element it is called on and changes focus to the specified element. | Nothing |
| getFullID | n/a | Gets the full ID of the element. | String: ID |
| getSoundSet | n/a | Returns the sound set being used on the element. | String: SoundSet |
| findSoundAlias | (String: Action) | Finds the corresponding sound alias to play from the sound set for the given action. | String: SoundAlias |
| playSound | (String: SoundAlias, *Unknown*) | *Plays the given sound alias. | Nothing |
| playActionSFX | n/a | Plays the action sound alias. | Nothing |
| setMouseDisabled | (Boolean: DisableMouse) | *Sets whether the element called on should handle the mouse (including move & click events). | Nothing |
| toggleMouse | n/a | Toggles whether the mouse should be disabled. | Nothing |
| setHandleMouse | (Boolean: HandleMouse) | Sets whether the element called on should handle mouse move & click events. | Nothing |
| toggleHandleMouse | n/a | Toggles whether the element called on should handle mouse move & click events. | Nothing |
| setHandleMouseMove | (Boolean: HandleMouseMove) | Sets whether the element called on should handle mouse move events. | Nothing |
| toggleHandleMouseMove | n/a | Toggles whether the element called on should handle mouse move events. | Nothing |
| setHandleMouseButton | (Boolean: HandleMouseButton) | Sets whether the element called on should handle mouse click events. | Nothing |
| toggleHandleMouseButton | n/a | Toggles whether the element called on should handle mouse click events. | Nothing |
| clearMouseFocus | n/a | Clears the current mouse focus. | Nothing |
| gainFocus | (UIElement: Element) | Plays the clips specific to gaining focus on the specified element. | Unknown |
| loseFocus | (UIElement: Element) | Plays the clips specific to losing focus on the specified element. | Unknown |
| processEvent | (Object: Event) | Processes an event on the element. | Nothing |
| processEventToParent | (Object: Event) | Processes an event on the parent element. | Nothing |
| getRoot | n/a | Gets the root parent element. | UIElement: Element |
| dispatchEventToRoot | (Object: Event) | Sends an event to the root element. | Nothing |
| dispatchEventToParent | (Object: Event) | Sends an event to the parent element. | Nothing |
| dispatchEventToParentWithSelf | (Object: Event) | Sends an event to the parent element, with reference to the source element called from. | Nothing |
| dispatchEventToParentWithElement | (Object: Event, UIElement: Element) | Sends an event to the parent element, with reference to the specified element. | Nothing |
| dispatchEventToChildren | (Object: Event) | Sends an event from a parent element to all of its children. | Nothing |
| registerEventHandler | (Object: Event, Function: Callback) | *Registers a callback for when an event is dispatched to it. | Nothing |
| isFocusable | n/a | *Returns whether the element called on is focusable. | Boolean: (true = Yes, false = No) |
| clearNavigationTable | n/a | Clears the current navigation on the given element. | Nothing |
| makeFocusable | n/a | *Makes the given element focusable. Clears current navigation on it. | Nothing |
| makeFocusableWithoutResettingNavigation | n/a | Makes the given element focusable. | Nothing |
| makeNotFocusable | n/a | Makes the given element not focusable. | Nothing |
| saveState | n/a | Saves the current state of the given element. | Nothing |
| clearSavedState | n/a | Clears the saved state of the given element. | Nothing |
| restoreState | n/a | Restores the saved state of the given element. | Nothing |
| hide | n/a | *Sets the element's alpha to 0. | Nothing |
| show | n/a | *Sets the element's alpha to 1. | Nothing |
| rotateRandomly | n/a | Applies a random X & Y rotation on the element. | Nothing |
| spinRandomly | n/a | Applies a random Z rotation on the element. | Nothing |
| setState | String: StateName, *Unknown* | Sets the given element to a state, and plays the associated clip if found. **Will be covered in a dedicated States / Clips guide** | Nothing |
| mergeStateConditions | Object: StateObject | Sets up the conditions for which to set each state. **Will be covered in a dedicated States / Clips guide** | Nothing |
| clipOver | n/a | Notifies that the current playing clip has ended, in order to play the next clip if queued. **Will be covered in a dedicated States / Clips guide** | Nothing |
| playClip | String: ClipName | Plays a clip specified in the clipsPerState object on the element. **Will be covered in a dedicated States / Clips guide** | Nothing |
| hasClip | String: ClipName | Returns whether the current state has a clip of this name. **Will be covered in a dedicated States / Clips guide** | Boolean: (true = Yes, false = No)
| setupElementClipCounter | Integer: Count | Specifies how many elements have clips to play before the clip is finished. **Will be covered in a dedicated States / Clips guide** | Nothing |
| clipFinished | Object: Event | Notifies that this child element has finished its individual clip. **Will be covered in a dedicated States / Clips guide** | Nothing |
| setClass | Object: ElementType | *Sets the class of this element. | Nothing |
| new | n/a | *Creates a new UIElement. | UIElement: Element |

## Examples
These examples assume that you have a somewhat decent grasp of LUI. You will not be spoonfed.

#### addElement
```lua
local CoffeeWidget = LUI.UIText.new()
CoffeeWidget:setText("Coffee is good")

Elem.coffeeWidget = CoffeeWidget
Elem:addElement(Elem.coffeeWidget)
```

#### linkToElementModel
```lua
CoffeeWidget:linkToElementModel(Elem, "displayText", true, function(ModelRef)
    local ModelVal = Engine.GetModelValue(ModelRef)

    if ModelVal then --Always, when handling a model subscription, do a nil check like this. You will get UI Errors otherwise.
        CoffeeWidget:setText(Engine.Localize(ModelVal)) --Sets the widget's text to the localized string for the value of the model.
    end
end)
```

#### subscribeToGlobalModel
```lua
--Code sourced from t7hud_zm_factory.lua - which was rebuilt by the D3V team (DTZxPorter, SE2Dev, Nukem). Credit them if you use this.
local function GumCallback(ModelRef)
    if IsParamModelEqualToString(ModelRef, "zombie_bgb_token_notification") then
        AddZombieBGBTokenNotification(HudRef, GumWidget, InstanceRef, ModelRef) -- Add a popup for a 'free hit'
    elseif IsParamModelEqualToString(ModelRef, "zombie_bgb_notification") then
        AddZombieBGBNotification(HudRef, GumWidget, ModelRef) -- Add a popup for the gum you got
    elseif IsParamModelEqualToString(ModelRef, "zombie_notification") then
        AddZombieNotification(HudRef, GumWidget, ModelRef) -- Add a popup for a powerup
    end
end

GumWidget:subscribeToGlobalModel(InstanceRef, "PerController", "scriptNotify", GumCallback)
```

#### close
```lua
LUI.OverrideFunction_CallOriginalSecond(Elem, "close", function(ObjRef)
    ObjRef.coffeeWidget:close()
end)
```

#### playSound
```lua
Elem:playSound("action") --Will play sound alias "action"
```

#### setMouseDisabled
```lua
Elem:setMouseDisabled("true") --Disables mouse events on element
```

#### registerEventHandler
```lua
Elem:registerEventHandler("transition_complete_keyframe", Elem.clipFinished) --In this example, the end of an animation is being used to alert a clip that one element has finished.
```

#### isFocusable
```lua
if CoffeeWidget:isFocusable() then
    CoffeeWidget:setText("Whey! We're focusable!")
else
    CoffeeWidget:setText("Bummer. We aren't focusable.")
end
```

#### makeFocusable
```lua
CoffeeWidget:makeFocusable() --Makes mouse work on it
```

#### hide
```lua
CoffeeWidget:hide() --Go away!
```

#### show
```lua
CoffeeWidget:show() --Come back!
```

#### setClass, new
```lua
CoD.List1ButtonLarge_ZM = InheritFrom(LUI.UIElement)

function CoD.List1ButtonLarge_ZM.new(HudRef, InstanceRef)
	local Elem = LUI.UIElement.new()
	if PreLoadFunc then
		PreLoadFunc(Elem, InstanceRef)
	end
	Elem:setUseStencil(false)
    Elem:setClass(CoD.List1ButtonLarge_ZM)
    --then rest of function
```

## End note
I cannot guarantee that all the information here is 100% accurate however I've done my best. Feel free to make edits, additions (particularly addition of examples) & corrections that you see fit.
