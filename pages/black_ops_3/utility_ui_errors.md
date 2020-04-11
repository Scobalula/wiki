---
title: UI Error Interception
keywords: blackops3, lui, utility
last_updated: 12th April 2020
credits: [Blak]
summary: "A guide on making use of a utility to intercept errors pushed within LUI, and provide more detail on those errors."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/utility_ui_errors.html
folder: black_ops_3
---

{% include note.html content="Do not expect this to stop `UI Error 1231878123` entirely! This will only provide you limited error information on `error()` calls pushed within LUI files." %}

## Setup
Download this LUI file: [ErrorInterception.lua](https://mega.nz/file/OFUxzapI#O2Ot2VIz3HQIHV_xByQN0z3guukvAXhtgI9BjW0k6J8)

Place this file in `usermaps/yourmapname/ui/utility/` and add to your zone: `rawfile,ui/utility/ErrorInterception.lua`.

Then in your `t7hud_zm_mapname` file, add `require("ui.utility.ErrorInterception")` at the top of the file.

## What now?
Whenever an `error()` function is called, within existing Black Ops III lua files or ones you add, instead of producing a typical UI Error with limited information, you will instead receive:
```
UI Error: Error message
```
Unfortunately this does not provide information on where the error is happening, but it should greatly help you to identify issues in cases where files are well coded to error if certain conditions aren't met for example.
