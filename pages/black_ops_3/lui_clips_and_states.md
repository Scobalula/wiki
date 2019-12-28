---
title: LUI Clips and States
keywords: blackops3, lui
last_updated: 28th December 2019
credits: [Blak]
summary: "A tutorial on how to make use of clips & states."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_clips_and_states.html
folder: black_ops_3
---

{% include note.html content="It is recommended to familiarise yourself with the more basic aspects of LUI such as model subscriptions before you follow this guide." %}

## What are clips and states?
**States** are as the name suggests, states that the element can take on. With states you can provide given conditions for each mode to be entered and you can get these conditions to evaluate using a model subscription.

**Clips** are actions for the element to do, as a result of `playClip` or a state being set. By default, regardless of state, the `DefaultClip` will play on that state.

These two things don't necessarily have to be used in conjunction, however most cases will tend to have them working in this way. This tutorial will cover how to use them in conjunction, how to use clips individually, and other bits and bobs, such as how to use animations with clips.

## Setting up clips
Clips are set up as a table under `Elem.clipsPerState`. When using clips, the parent element should be what `clipsPerState` is called on, and its children are what get affected in the clip functions. Therefore, you could use it on simply `Elem` within a widget, or otherwise on a child widget within that file if that child widget has more children within its element.

Here is an example of a clip setup:
```lua
Elem.clipsPerState = {
    DefaultState = { --DefaultState is the element state if no other condition is met.
        DefaultClip = function() --This is the default clip to play for this specified state.
            Elem:setupElementClipCounter(2) --This function tells the clip handler to expect 2 calls of clipFinished() before it can say that the clip has ended.

            CoffeeWidget:completeAnimation() --Finishes any animation transition currently occuring on the element. If the animation has been tied to an event, it will pass interrupted onto the Event object (Covered later).
            Elem.coffeeWidget:setAlpha(1) --Do whatever we want this clip to do

            Elem.clipFinished(CoffeeWidget, {}) --The specific part of the clip for CoffeeWidget has finished, so we can call this.

            TeaWidget:completeAnimation()
            Elem.teaWidget:setAlpha(0) --Do whatever we want this clip to do

            Elem.clipFinished(TeaWidget, {}) --The specific part of the clip for TeaWidget has finished, so we can call this.
        end
    }
}
```

Always, when doing clips, ensure you have `setupElementClipCounter`, `clipFinished` and `completeAnimation`. They all have substantially important roles.

This example only covers 1 state at the moment. Let's add another.

```lua
Elem.clipsPerState = {
    DefaultState = { --DefaultState is the element state if no other condition is met.
        DefaultClip = function() --This is the default clip to play for this specified state.
            Elem:setupElementClipCounter(2) --This function tells the clip handler to expect 2 calls of clipFinished() before it can say that the clip has ended.

            CoffeeWidget:completeAnimation() --Finishes any animation transition currently occuring on the element. If the animation has been tied to an event, it will pass interrupted onto the Event object (Covered later).
            Elem.coffeeWidget:setAlpha(1) --Do whatever we want this clip to do

            Elem.clipFinished(CoffeeWidget, {}) --The specific part of the clip for CoffeeWidget has finished, so we can call this.

            TeaWidget:completeAnimation()
            Elem.teaWidget:setAlpha(0) --Do whatever we want this clip to do

            Elem.clipFinished(TeaWidget, {}) --The specific part of the clip for TeaWidget has finished, so we can call this.
        end
    },
    TheyPreferTeaState = {
        DefaultClip = function() --This is just like the function above except I've changed each element's alpha.
            Elem:setupElementClipCounter(2)

            CoffeeWidget:completeAnimation()
            Elem.coffeeWidget:setAlpha(0)

            Elem.clipFinished(CoffeeWidget, {})

            TeaWidget:completeAnimation()
            Elem.teaWidget:setAlpha(1)

            Elem.clipFinished(TeaWidget, {})
        end
    }
}
```

Now, if the conditions of `TheyPreferTeaState` are met, that function will instead run, meaning that the `CoffeeWidget` will be hidden and the `TeaWidget` will be shown. Likewise, if it's not met, then `CoffeeWidget` will show and `TeaWidget` will hide (`DefaultState`). Now that we've started to dabble with clips in each state, let's now go on to how to use states;

## Setting up states
To set up states, you need to use the function `mergeStateConditions`, passing a table to it. Here's an example setup:

```lua
Elem:mergeStateConditions({
    {
        stateName = "TheyPreferTeaState", --Tell the game which state you want it to use if the condition is met
        condition = function(arg1, arg2, arg3) --Condition function
            if (Your condition here) then --Pass a condition through here that you want met, such as a model value, engine function, etc.
                return true --Do use this state
            else
                return false --Do NOT use this state
            end
        end
    }
})
```

From here, you could add more states and more conditions should you wish to. Note that you do not have to have a specific setup for `DefaultState`, it will be set if all other conditions are not met.

Now that you have your clips and states outlined, you need a way to update them:

## Updating the element state
To update the element state, you use a model subscription on `Elem`. Here is an example state update function.

```lua
Elem:subscribeToModel(Engine.GetModel(Engine.GetModelForController(InstanceRef), "UIVisibilityBit." .. Enum.UIVisibilityBit.BIT_SCOREBOARD_OPEN), function(ModelRef) --Here a model subscription has been made (to a UIVisibilityBit)
    HudRef:updateElementState(Elem, {name = "model_validation", --You are calling for HudRef (the first argument on CoD.xyxyxyxy.new() to update the main element).
        menu = HudRef, modelValue = Engine.GetModelValue(ModelRef),
        modelName = "UIVisibilityBit." .. Enum.UIVisibilityBit.BIT_SCOREBOARD_OPEN}) --Repeat the model here.
end)
```

This allows the state conditions to re-evaluate when `"UIVisibilityBit." .. Enum.UIVisibilityBit.BIT_SCOREBOARD_OPEN` changes. The principle is the same for any model.

## Using clips exclusively
Let's go back to our original clip setup, and instead of adding another state, add another clip.
```lua
Elem.clipsPerState = {
    DefaultState = { --DefaultState is the element state if no other condition is met.
        DefaultClip = function() --This is the default clip to play for this specified state.
            Elem:setupElementClipCounter(2) --This function tells the clip handler to expect 2 calls of clipFinished() before it can say that the clip has ended.

            CoffeeWidget:completeAnimation() --Finishes any animation transition currently occuring on the element. If the animation has been tied to an event, it will pass interrupted onto the Event object (Covered later).
            Elem.coffeeWidget:setAlpha(1) --Do whatever we want this clip to do
            Elem.coffeeWidget:setScale(1) --Added this to ensure it resets after BeSmall

            Elem.clipFinished(CoffeeWidget, {}) --The specific part of the clip for CoffeeWidget has finished, so we can call this.

            TeaWidget:completeAnimation()
            Elem.teaWidget:setAlpha(0) --Do whatever we want this clip to do
            Elem.teaWidget:setScale(1) --Added this to ensure it resets after BeSmall

            Elem.clipFinished(TeaWidget, {}) --The specific part of the clip for TeaWidget has finished, so we can call this.
        end,
        BeSmall = function() --Other clip in DefaultState, BeSmall
            Elem:setupElementClipCounter(2)

            CoffeeWidget:completeAnimation()
            Elem.coffeeWidget:setScale(0.5) --This clip shrinks the scale of the two widgets.

            Elem.clipFinished(CoffeeWidget, {})

            TeaWidget:completeAnimation()
            Elem.teaWidget:setScale(0.5) --This clip shrinks the scale of the two widgets.

            Elem.clipFinished(TeaWidget, {})
        end
    }
}
```

Here now we could add a `Elem.playClip("BeSmall")` somewhere in our LUI and it would, instead of playing DefaultClip, play this. However, in this current setup, you probably wouldn't even notice a difference: The clip would only play once and instantly, then it would revert back to DefaultClip. This is where animations come to use.

## Using animations with clips
Here is a modified version of the clip above. TeaWidget functionality has been omitted.
```lua
Elem.clipsPerState = {
    DefaultState = { --DefaultState is the element state if no other condition is met.
        DefaultClip = function() --This is the default clip to play for this specified state.
            Elem:setupElementClipCounter(1) --This function tells the clip handler to expect 2 calls of clipFinished() before it can say that the clip has ended.

            CoffeeWidget:completeAnimation() --Finishes any animation transition currently occuring on the element. If the animation has been tied to an event, it will pass interrupted onto the Event object (Covered later).
            Elem.coffeeWidget:setAlpha(1) --Fade back in
            Elem.coffeeWidget:setScale(1) --Restore scale

            Elem.clipFinished(CoffeeWidget, {}) --The specific part of the clip for CoffeeWidget has finished, so we can call this.
        end,
        BeSmall = function() --Other clip in DefaultState, BeSmall
            Elem:setupElementClipCounter(1)

            CoffeeWidget:completeAnimation()

            Elem.coffeeWidget:beginAnimation("keyframe", 500, false, false, CoD.TweenType.Linear) --Start a linear keyframe animation that lasts 500ms.
            Elem.coffeeWidget:setScale(0.5) --This clip shrinks the scale of the two widgets. Due to the animation, this will occur over 500ms.

            Elem.coffeeWidget:registerEventHandler("transition_complete_keyframe", Elem.clipFinished) --Now LUI will only be notified once the transition has ended that this clip is finished. 2 arguments are passed (Element, Event)
        end
    }
}
```

Ok, cool. But now when the smooth animation ends on BeSmall, it will still instantly revert back to 1x scale. What if, within the clip, we animate it again to restore its scale?

## Using multiple animations within a clip
```lua
Elem.clipsPerState = {
    DefaultState = { --DefaultState is the element state if no other condition is met.
        DefaultClip = function() --This is the default clip to play for this specified state.
            Elem:setupElementClipCounter(1) --This function tells the clip handler to expect 2 calls of clipFinished() before it can say that the clip has ended.

            CoffeeWidget:completeAnimation() --Finishes any animation transition currently occuring on the element. If the animation has been tied to an event, it will pass interrupted onto the Event object (Covered later).
            Elem.coffeeWidget:setAlpha(1) --Fade back in
            Elem.coffeeWidget:setScale(1) --Restore scale

            Elem.clipFinished(CoffeeWidget, {}) --The specific part of the clip for CoffeeWidget has finished, so we can call this.
        end,
        BeSmall = function() --Other clip in DefaultState, BeSmall
            Elem:setupElementClipCounter(1)

            CoffeeWidget:completeAnimation()

            Elem.coffeeWidget:beginAnimation("keyframe", 500, false, false, CoD.TweenType.Linear) --Start a linear keyframe animation that lasts 500ms.
            Elem.coffeeWidget:setScale(0.5) --This clip shrinks the scale of the two widgets. Due to the animation, this will occur over 500ms.

            Elem.coffeeWidget:registerEventHandler("transition_complete_keyframe", function(Element, Event) --This function will run when the animation ends.
                --Elem.coffeeWidget is passed to this function as Element, so for simplicity's sake we'll use that.
                if not Event.interrupted then --If the animation was not interrupted by a completeAnimation() call, i.e. another clip playing, let's go on animating.
                    Element:beginAnimation("keyframe", 500, false, false, CoD.TweenType.Linear)
                end
                --Regardless of whether we were interrupted or not, restore scale, either instantly or over time.
                Element:setScale(1)
                if Event.interrupted then --If we were indeed interrupted, let's finish the clip here.
                    Elem.clipFinished(Element, {})
                else --If not, then let's wait for the animation to end, and then notify that the clip is finished.
                    Element:registerEventHandler("transition_complete_keyframe", Elem.clipFinished)
                end
            end)
        end
    }
}
```

Here you can see the necessity for using `completeAnimation()`. If another clip's animation is playing, you need to stop it and get that clip to end. Within this clip, we've added checks for whether the first transition was interrupted, so that we can end half-way through if so. We don't need to do this on the second animation as `clipFinished` will be called at whatever point the animation ends at.

## A final miscellaneous bit - looping a clip
Let's say you want to have your clip repeat, for example you could have a low ammo repeated color change on your HUD that you want. Here's how you could do it:
```lua
Elem.clipsPerState = {
    DefaultState = {
        FancyClip = function()
            Elem:setupElementClipCounter(1)

            CoffeeWidget:completeAnimation()
            
            Elem.coffeeWidget:setRGB(1, 1, 1) --Set to 255, 255, 255

            Elem.coffeeWidget:beginAnimation("keyframe", 500, false, false, CoD.TweenType.Linear)

            Elem.coffeeWidget:setRGB(1, 0, 0) --Set to 255, 0, 0

            Elem.coffeeWidget:registerEventHandler("transition_complete_keyframe", function(Element, Event)
                if not Event.interrupted then
                    Element:beginAnimation("keyframe", 500, false, false, CoD.TweenType.Linear)
                end
                Element:setRGB(1, 1, 1) --Set to 255, 255, 255
                if Event.interrupted then
                    Elem.clipFinished(Element, {})
                else
                    Element:registerEventHandler("transition_complete_keyframe", function(Element2, Event2) --We're doing another function here to check if the second part was interrupted... 
                        if not Event2.interrupted then
                            Elem.playClip("FancyClip") --Play this clip again, as we weren't interrupted!
                        end
                        Elem.clipFinished(Element2, {}) --Clip is finished
                    end)
                end
            end)
        end
    }
}
```

In essence, `completeAnimation()` ends up becoming a notifier to any clips playing to stop, and so you can take advantage of this to loop your clip so long as it does not at any point get interrupted. If you want to do a looping clip with multiple elements having functionality in, ensure that whatever element finishes last is the one to call the clip again.
