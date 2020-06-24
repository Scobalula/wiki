---
title: Inverse Kinematics (IK)
keywords: blackops3, animation
last_updated: 24th June 2020
credits: [Blak, Scobalula, Thomas Cat]
summary: "A guide on how to apply Inverse Kinematics in Maya."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/inverse_kinematics.html
folder: black_ops_3
---

## Information
### What is Inverse Kinematics (IK)?
Traditionally, you are used to the idea of Forward Kinematics (FK). Adjusting a parent joint will affect its children, which in turn those children being adjusted will affect their children and so on. Moving a child joint has no impact on its parent joints.

This is where Inverse Kinematics come in. Like the name suggests, it is the opposite to Forward Kinematics. Moving a child joint will impact its parent joints, which will impact their parents, etc. Moving a wrist will adjust the elbow in accordance. If you have ever used custom animation rigs - you will have used IK before, either in moving a wrist into an animation pose, or the gun movement affecting the wrists (which then affect the elbows etc.).

### What are the applications of IK?
There are multiple uses for IK for example if you are modding Black Ops III. To briefly describe 2 uses:
* MW2019 weapons use IK for wrist positioning in relation to the weapon. While some MW2019 weapons are fine without IK, there are others that experience unusual jitter without IK applied. As Black Ops III does not support First Person IK, you must add this yourself in Maya. Indeed, some weapons won't even have correct base wrist positions without IK applied...
* You may want to do generic additive animations and/or edit existing animations. There are cases where wrist to gun movement will appear off, and IK can help you fix this.

## How to use IK

### IK joints
If you are not porting an MW2019 weapon, you do not have joints pre-prepared. Create joints `tag_ik_loc_le` and `tag_ik_loc_ri` under `j_gun/tag_weapon` and position them to be at the same position as your `j_wrist_le` and `j_wrist_ri` joints respectively.

### Preparing scene for IK
{% include note.html content="You may want to implement this into a shelf to save yourself re-entering this every time." %}

First we must tell Maya that we would prefer the pole vector of the elbow to be positioned in its current place. The following code will set the preferred angle for the shoulder and elbow joint chain to be how it is presently (so apply this with an animation imported). Copy and paste this code into your Maya's command line:

```
joint -e -spa -ch j_elbow_le j_shoulder_le; joint -e -spa -ch j_shoulder_ri j_elbow_ri
```

### Applying IK
First, go to Skeleton -> Create IK Handle (box). Ensure it is on these settings:

![](https://i.gyazo.com/b9f334d31183b96f45e6915da78ef0f1.png)

Next, go to Skeleton -> Create IK Handle. In the 3D view, select first your start joint as `j_shoulder_x`, then select your end effector as `j_wrist_x`, where `x` is the side you are doing. This will create an IK handle.

Repeat this last point for the other side.

### Constraining the wrists and IK for gun movement

Now that you have created your IK handles, for each one you need to do some constraining. Select a side's IK handle, then select `j_wrist_x`, and go to Constrain -> Orient (box). Ensure that Maintain Offset is checked, and apply. Repeat this for the other side.

Then, select your `tag_ik_loc_x`, then select your side's IK handle and do Constrain -> Orient, again with Maintain Offset ticked. Finally, select these two again in the same order, and do Constrain -> Point (box). It is crucial here to know whether you want your wrist to move to the IK loc joint position (most likely in MW2019 cases), or not. If you want it to move, leave Maintain Offset **unticked**, if you do not want it to move, **tick** Maintain Offset.

Now your player's arms should accurately follow the weapon movement. When you are doing your next animation, simply delete both IK handles to effectively "reset" things ready for another animation to be dragged in.

## Blending between IK and FK
For certain animations you will need to blend between IK and FK (such as reloads).

### Full IK
Where you need your wrist to be following the gun movement, set a keyframe on the IK handle on the `ikBlend` attribute, setting its value to 1. Additionally, on your wrist joint, set a keyframe on the `blendOrient1` attribute, also to value 1.

### Full FK
Where you need your wrist to be independent of gun movement, set a keyframe on the IK handle on the `ikBlend` attribute, setting its value to 0. Additionally, on your wrist joint, set a keyframe on the `blendOrient1` attribute, also to value 0.