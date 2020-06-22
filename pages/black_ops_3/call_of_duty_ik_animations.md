---
title: Using Call of Duty IK Anims
keywords: blackops3, animation, ik, porting
last_updated: 17th November 2019
credits: [ThomasCat]
summary: "This tutorial will demonstrate how to use Call of Duty IK anims in Maya."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/call_of_duty_ik_animations.html
folder: black_ops_3
---

{% include danger.html content="**This guide has been archived and so therefore is no longer supported or recommended.** There will be a guide to replace this one at some point in future." %}

{% include important.html content="If you want to be able to do IK anims you need to have the necessary knowledge in Maya and a basic understanding of inverse and Forward kinematics aswell as animation layers." %}

{% include note.html content="You will need: [Greyhound](https://github.com/Scobalula/Greyhound/releases), [Autodesk Maya](https://www.autodesk.com/education/free-software/maya), A set of viewhands from the game the IK anims are from and [SETools](https://github.com/dtzxporter/SETools)." %}

## Deciding what anims are IK

Sometimes you may spot an animation that looks really funky and not know how to import it correctly, you may even blame yourself or the exporter for it not working correctly. This is usually an IK anim.

You can tell if it is an IK animation if:

* Hands are straightened out
* One arm stays in the bind pose
* The arms are animated but move around a wierd pose

Usually these IK anims only show up in Infinite Warfare and up.

These anims could be:

* Grip
* Walk
* Sprint, Super Sprint & Sprint Offsets
* Empty Addatives
* ADS Addatives

Now we have decided what animations we need to apply this for we can get to work. There are three different methods for different situations. One is for the Grip IK anims, the other is for IK anims that can offset or not offset the shoulder and the last is a combination of the second method and using IK handles. As you can see IK anims are nothing but addative anims with extra steps, no wonder they're used so much!

## Grip IK Animations

First of all, this method is tested and works with MW2019 and BO4. If you are trying a grip anim from a different game than the results may not be the same as mine.

Drag on the IK grip animation. I'm going to use a shotgun from MW to test but it works exactly the same as BO4 does just with a different pose when you drag it on.

Mine looks like this:


![Grip Ik Anim](https://i.imgur.com/vSAHsOu.jpg)

This may look wierd but this is perfectly natural. Imagine this movement is overlayed directly ontop of the original animation. Incase you haven't noticed, this is the exact purpose of an animation layer. Now, select every joint and every frame in the timeline then copy it and import your idle. You should now just see the normal idle animation.

Now select every joint then head over to this tab on the bottom right:


![Anim Layer Tab](https://i.imgur.com/MZAcczT.jpg)

Click Layers, then select `Create Layer From Selected`. This will create a new anim layer and the anim layer stack will now look like this:


![Anim Layer Stack](https://i.imgur.com/zNxRh23.jpg)

Then right click `AnimLayer1` and click `Rotation Accumulation - By Layer`. This will fix the broken rotates that would occur if you where to apply the IK animation right now.

Now, with the anim layer selected, paste the frames that we copied from the grip IK animation onto the timeline. With any luck, the hand should jump to the correct position for the grip!

This is my end result on the idle animation for the shotgun:


![Shotgun Grip Idle](https://i.imgur.com/MyWe699.jpg)

Sometimes, you will need to animate the blend between the normal animation and the grip animation. You can do this by keying the weight. You do this by using these two buttons:


![Anim Layer Weight Key Buttons](https://i.imgur.com/rzVhsVd.jpg)

The zero with the plane underneath it will key the lower layer (original animation) and the one with the plane underneath it will key the layer your on (the grip animation). Usually you will want to key to zero  just after the hand leaves the gun and key to one just before the hand leaves the weapon.

This is what the `reload_end` animation looks for the weapon I'm working with:


![Shotgun Reload End Grip IK](https://i.imgur.com/FEFSC86.gif)

## Normal IK Animations

Do the same thing as before and import the weapon onto a set of viewhands. In my case, I'm going to be using the IW Stallion .44 ADS addative animation (This would then be used to blend in the sprints so the hand goes into the correct pose, just like ingame).

Then Import the IK animation. Mine looks like this:


![.44 Stallion ADS Addative IK Anim](https://i.imgur.com/qR2bTY7.jpg)

Then select and copy all of the frames and remember the frame count. In my case the animation ends on the ninth frame. Now, import idle, select all of the joints, and create an anim layer using the same method as before. Then, with all the frames still selected and the anim layer selected, paste in the frames you copied before.

This is what my final result looks like:


![.44 Stallion ADS Addative IK Anim Done](https://i.imgur.com/z2mspGL.gif)
## Advanced IK Animations

{% include warning.html content="You will definately need alot of experience with Maya and be comfortable with animation layers to be able to follow this guide. If you are struggling with either of these, look up an animation layer tutorial online." %}

Next, put the gun on the rig again. In this guide I will be using my shotgun again as a example. Then, import the IK animation you want to use. I will be using the IK walk animation. Then select all of the joints, copy the frames, and take note of the frame count (mine is 112). Import idle then select all joints and create an anim layer the same as before. Paste the IK animation in. You may notice so issues (In my case, the right clavicle is offset and so is the weapon). Lets fix that.

Mute `AnimLayer1` and select the `BaseAnimation` layer. The mute button is here:


![Mute Button](https://i.imgur.com/f2rZ49N.jpg)

Duplicate the offset clavicle you have. Mine is the right clavicle so I will refer to it as the right clavicle from now on. So then I duplicate the right clavicle and delete all of the child joints and unmute `AnimLayer1`. Then select the original right clavicle then the duplicate of the right clavicle (notice how it is at the correct offset). Then head over to the `Rigging` tab found here:


![Rigging Tab](https://i.imgur.com/0CniSB6.jpg)

{% include warning.html content="Make sure to parent at the first frame / when the gun is at its idle animation otherwise the entire shoulder movement will be slightly offset and look completly incorrect." %}

With the joints still selected in the correct order from before, click the following: `Constraint - Parent - The box next to it`. Use these exact settings:


![Parent constraint settings 1](https://i.imgur.com/Bclr70x.jpg)

Click apply.

Then go to the animation tab here:


![Animation Tab](https://i.imgur.com/YhpQ2kH.jpg)

Now, select the duplicate right clavicle joint and click `Key - Bake Animation`. Once that's done, delete the parent constraint.


![Parent Constraint](https://i.imgur.com/hSub5LD.jpg)

Then select the original right clavicle and type `cutKey` into the MEL script box **NOTE THAT IT IS CASE SENSITIVE**


![MEL Script Box](https://i.imgur.com/eoJWMkG.jpg)

Now select the right clavicle then the duplicate right clavicle joint and parent constraint again but with these settings:


![Parent constraint settings 2](https://i.imgur.com/H2Zn6lT.jpg)

Now, the only thing left that is broken is the weapon position for me. To fix this select tag_weapon left and then tag_weapon and parent with the same settings we used to parent the duplicate right clavicle joint to the original right clavicle joint.

{% include note.html content="The joint you parent to tag_weapon depends on the rig and the way the animation works. With the knowledge you hopefully have with Maya you should be able to adapt to this." %}

This is my final result:


![Advanced IK animation Result](https://i.imgur.com/AOwychf.gif)

## Advanced IK Animations with IK Handles

You may have noticed the hand doesn't exactly line up sometimes once you complete the final step on the last section. To fix this, we use IK handles that are parented to the IK joint under the weapon. Here is an example of the line not lining up correctly:


![Hand not lining up](https://i.imgur.com/l8L0jWy.gif)

Ok, so lets fix this! First, select the right shoulder (j_shoulder_ri) then click `Select - Hierarchy` and type `cutKey` in the MEL script box.

Then paste in the corresponding code into the MEL script box depending on which shoulder you are wanting to line up.

```mel
joint -e -spa -ch j_elbow_le j_shoulder_le
joint -e -spa -ch j_shoulder_ri j_elbow_ri
```

I'm working with the right shoulder so I'm going to psate in the one for the right shoulder. Now, go to the rigging tab and click `Skeleton - Create IK Handle`.

Once you have done that, double click this on the left tool bar


![IK Handle Tool Button](https://i.imgur.com/hu9fp3o.jpg)

Change the settings to the same as mine on the window popup


![IK Handle Settings](https://i.imgur.com/oqXxQ68.jpg)

{% include note.html content="You can enable the Joint X-ray option to easily see the joints using this button:" %}

![Joint Xray](https://i.imgur.com/VxzmtyM.jpg)

{% include note.html content="Make sure you do everything from here on the first frame." %}

Click the shoulder joint with the IK handle tool, my shoulder joint is located here:


![Shoulder Joint](https://i.imgur.com/D80qerI.jpg)

Then click the wrist, mine is located here:


![Wrist Joint](https://i.imgur.com/3sY20Nv.jpg)

{% include note.html content="Clicking on the correct joint can be fiddly and you may have to do it multiple times until its correct. To combat this, you can hide joints you don't need to see using H to hide and Shift-H to unhide" %}

Select `ikHandle1` and the corresponding wrist joint. In my case, it's `j_wrist_ri`. Then click `Constraint - Orient - The box next to it` and use these settings:


![Orient Constraint Settings](https://i.imgur.com/EhBQvdL.jpg)

Click apply.

Select the right IK joint under the weapon (mine is called `tag_ik_loc_ri`) then select `ikHandle1`. Click `Constraint - Parent - The box next to it`. Then tick maintain offset and apply.

This is my final result:


![IK Handle Advanced IK Animations Final Result](https://i.imgur.com/V0aKf5O.gif)

## Finished!

Now with all of this information in mind, you can now apply all of this to games like Apex Legends or in the variaties in other animations such as Super Sprint IK anims. There are slight variaties between each animation and between each animation, this is why I suggest you have alot of experience with Maya and you look up some tutorials before following this tutorial.

{% include warning.html content="If you have any issues then please don't bother everyone with it and don't bother me with it as you likely don't have the required knowledge in Maya to figure it out. If you can follow along with the same models and anims I used here and have a decent understanding and find something wierd / interesting that is broken, talk to me about it on discord, my discord tag is: `Thomas Cat#7648`" %}
