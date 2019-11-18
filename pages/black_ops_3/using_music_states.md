---
title: Using Music States
keywords: blackops3, mapping, ambient, audio
last_updated: 16th November 2019
credits: [Blak, Scobalula]
summary: "This tutorial will demonstrate how to make use of Music States."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/using_music_states.html
folder: black_ops_3
---

## Setting up a .mus file

In order to make use of the music system you need to create a .mus file in `Call of Duty\share\raw\sound\music`. We are not provided an example file by default so it is recommended you rip a music file from a map using [HydraX](https://github.com/Scobalula/HydraX/).

With a .mus file ripped from the game or otherwise, name it to something relevant (such as your map name). Then, open it, and find the first `"Name"` parameter where you again need to set its value to the file name you have chosen (without the extension).

Now, find your map's sound zoneconfig `map folder\sound\zoneconfig\mapname.szc`. Open it, and find `"MusicFiles"`. Within its value array, enter the name you chose for your .mus file.

{% include note.html content="The parts of your .mus that need editing will be gone through later in the tutorial, this is just the basics for now." %}

## Setting up aliases to work with music states

{% include note.html content="It is recommended to use [HydraX](https://github.com/Scobalula/HydraX/) to rip existing music aliases from the game for correct settings." %}

There isn't anything massive that needs to be done to your aliases to make them work with the music state system, however there is a namescheme that **must** be observed:
`mus_ + ALIAS NAME YOU WANT + _intro`
So for example my alias could be called `mus_roundstart_potato_famine_intro`.

While you can technically call any alias name from the music state system, the reason you must use the name scheme is because the `mus_` + `_intro` naming is hardcoded into the `_zm_audio.gsc` script, and the script will have playback time-related issues if you don't use the name scheme.

## Registering your music states

{% include important.html content="If you want to override the music states for round sounds, etc, it is necessary to call your music state create functions after `zm_usermap::main()`." %}

In any file where you are going to register music states, it is recommended to add these define calls:
```
#define PLAYTYPE_REJECT 1
#define PLAYTYPE_QUEUE 2
#define PLAYTYPE_ROUND 3
#define PLAYTYPE_SPECIAL 4
#define PLAYTYPE_GAMEEND 5
```

To register a music state, use this function:
```
zm_audio::musicState_Create(stateName, playType, musName1, musName2, musName3, musName4, musName5, musName6 );
```

**stateName** - a script reference for the music track, you have pretty much any scope to name this, however do note that you must name this e.g. `"round_start"` if you want to painlessly change round sounds.

**playType** - There are five play types that you can use here which determines the priority and nature of the music. Do note that without the define calls above, you cannot use these references specifically.
* `PLAYTYPE_REJECT` - This music will only play if no other music is playing at the time. (Lowest priority)
* `PLAYTYPE_QUEUE` - This music will be queued to play after other tracks. Example of use is The Giant power music. (Low priority)
* `PLAYTYPE_ROUND` - Self-explanatory, used for round sounds. (Mid priority)
* `PLAYTYPE_SPECIAL` - This music will stop round sounds playing along with anything else below it. The common use for this is Easter Egg songs. (High priority)
* `PLAYTYPE_GAMEEND` - This music will stop all other music tracks and will play with no disruptions. This is designated for game over. (Highest priority)

**musName1-6** - This is a reference to the .mus song entry. This must be named to your alias MINUS `mus_` and `_intro`. You do not have to use any more than one, multiple ones are for randomising like The Giant round start sounds.

## Setting up a music track in your .mus file

Go to your .mus file that you created earlier in the tutorial. Go to the `StateArray`.

Below is an example `StateArray` entry.

```json
{
    "Name": "roundstart_potato_famine",
    "IntroAsset": {
        "AliasName": "mus_roundstart_potato_famine_intro",
        "Looping": false,
        "CompleteLoop": false,
        "RemoveAfterPlay": false,
        "PlayAsFirstRandom": false,
        "StartSync": false,
        "StopSync": false,
        "CompleteOnStop": false,
        "LoopStartOffset": 15662,
        "BPM": 120,
        "AssetType": 0,
        "LoopNumber": 1,
        "Order": 0,
        "StartDelayBeats": 0,
        "StartFadeBeats": 0,
        "StopDelayBeats": 0,
        "StopFadeBeats": 4,
        "Meter": 4
    },
    "LoopAssets": [],
    "Order": 0,
    "IsRandom": false,
    "IsSequential": true,
    "SkipPreviousExit": false
}
```

You will need to create a `StateArray` entry for every one of your music tracks that you've put as a `musName`.

This is what you need to change the values of from the template above for an entry:
* `"Name"` - Set this one's value to the `musName` you have in your script create state call.
* `"AliasName"` - Set the value of to your actual alias' name.
* Second `"Order"` - This one isn't necessary, but I have noted that Treyarch do this as an index from 0 of entries within the state array, so change it to reflect this if you want.

Next, you need to go to the bottom of your .mus file, and find `"StateNames"`. In this array, add an entry string to say your `musName`, such as `"roundstart_potato_famine"`.

## Playing a music state

This step is simple enough, use this function:
```level thread zm_audio::sndMusicSystem_PlayState(stateName);```
where `stateName` is the script name you set in your create state function.


## Complete

Assuming you've followed all the steps, everything should be working in-game, but I'm also braindead so maybe I missed something. thx