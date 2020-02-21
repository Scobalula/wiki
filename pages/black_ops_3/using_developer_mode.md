---
title: Using Developer Mode
keywords: blackops3, scripting
last_updated: 21st February 2020
credits: [Blak, Scobalula, Ardivee]
summary: "A guide on making use of developer mode to polish your scripts."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/using_developer_mode.html
folder: black_ops_3
---

## Introduction
One of the most crucial things to do when you are scripting is test the script with developer mode on. Developer mode allows you to catch various issues relating to your script which you need to polish and fix to ensure your code behaves properly.

Many choose to ignore developer mode, believe it doesn't matter, but it should not be ignored. Developer errors are very capable of causing unintended issues and the worst ones can script crash the game (Connection Interrupted). It's a misconception that only a loop without a pause inside it can cause a script crash, so can developer errors.

Having a broken developer mode isn't an easy anti-cheat, stop being lazy.

## How to thoroughly test your script
If you want to test your script and catch any potential issue right from the start, there are four commands to use either in console if launching from lobby, or four arguments to enter below Run in Launcher.

Developer 2: Lobby `/developer 2`, Launcher `+developer 2` - Enables the baseline issue catching

Logfile 2: Lobby `/logfile 2`, Launcher `+logfile 2` - Writes a logfile to `mods/modormapname/console_mp.log`, so you can refer to errors from there following a playthrough

Devblock: Lobby `/scr_mod_enable_devblock 1`, Launcher `+set scr_mod_enable_devblock 1` - Enables `Assert()` functions and code wrapped in a devblock `/# #/`, which will help you to catch issues.

Clientfield debug: (NOT AVAILABLE FROM LOBBY), Launcher: `+set com_clientfieldsDebug 1` - If you have a clientfield mismatch issue, this will report what is mismatching and where.

## Ok, I got an error, what now?
Developer mode will give you somewhat of an idea what the issue is and will normally tell you roughly what line the issue is on. You'll need to have a level of proficiency in GSC/CSC to understand what is the issue or how to fix it, and if you don't know what it's telling you, just ask someone more experienced. (but not hb)