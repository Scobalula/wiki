---
title: Using UILists & Datasources
keywords: blackops3, lui
last_updated: 1st January 2020
credits: [Blak, Scobalula, lilrifa, JariK]
summary: "A guide on how to make use of datasources on UI Lists."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_uilists_datasources.html
folder: black_ops_3
---

## Foreword

On list elements (`UIList`), data sources can be used to create listed elements, repeated but different. For this a data source is needed (created from a data table), a list item widget that can interpret the data source is needed, and the `UIList` itself.


## Setting up a UIList

{% include note.html content="The meaning of every argument of `UIList` is not currently fully known. However, this is the general idea: `(HudRef, InstanceRef, Spacing, Unknown, Filter, Unknown, Unknown, Unknown, Unknown, Unknown, Unknown)`. It's possible the last 6 arguments are related to positioning, however one can only be sure via testing..." %}

We'll start here as it will make more sense as we come to setting up our data source. Here is how you setup your `UIList`:
```lua
local SectionsList = LUI.UIList.new(HudRef, InstanceRef, 2, 0, nil, false, false, 0, 0, false, false)
SectionsList:setWidgetType(CoD.SectionListButton)
SectionsList:setVerticalCount(5)
SectionsList:setDataSource("SectionListDataSource")

HudRef:addElement(SectionsList)
```
This is the bare minimum required for setting up a `UIList`. Of course, just like any other element, you can set positioning, etc, with the relevant functions.

On the first line we have created the list with spacing 2 between each element. On the second line we've told LUI that we will be using widgets with class `CoD.SectionListButton` as our list items, so this is the widget we need to set up for our data source. The third line sets the amount of elements that will be shown vertically at any given time. You could then on top of this add a scrollbar and scroller if you wanted to allow you to have more elements whilst only listing a set amount (not covered in this guide). Then the fourth line sets the data source and tells LUI to get the list items that have been created in that data source. Then finally we've added the list to our HUD.

So, to recap, we'll be using a data source that we'll call `SectionListDataSource` and a widget with class `CoD.SectionListButton`. Let's now make those.

## Structure of a data table for a DataSource

The contents within a data table can vary from data source to data source, but all data sources are built on two similar principles.

Here is an example of a simple, one element data table for a data source:
```lua
local DataTable = {
    {
        models = {
            buttonText = "Zombies",
            disabled = true
        },  
        properties = {
            section = "zm"
        }
    }
}
```

With this now displayed, let's explain it;

Element **models** are sent to the each correspondent list element widget and can be accessed via a `linkToElementModel` model subscription. For example:
```lua
ButtonText:linkToElementModel(Elem, "buttonText", true, function(ModelRef)
    local ModelVal = Engine.GetModelValue(ModelRef)
    if ModelVal then
        ButtonText:setText(Engine.Localize(ModelVal)) --Now, for each sub-table of DataTable sent to the data source, the model buttonText will be applied to the list element widget.
    end
end)
```

Whereas, element **properties** are added onto `Elem` itself, and can be accessed like this:
```lua
Elem.section --This is all we need to access "zm"
--Or you could use:
Elem["section"] --Both of these are the same thing.
```

The cases for each to be used differ. You'd use models to setup the characteristics of how you want your widget to behave or display, whereas you'd use properties to store information related to the element, for example if you wanted it to do something when selected but need to access certain data for this.

## Creating a DataSource from a data table

To create a data source, we add our data source name to the `DataSources` object, and use the `DataSourceHelpers.ListSetup` function to create it. Like so:
```lua
DataSources.SectionListDataSource = DataSourceHelpers.ListSetup("SectionListDataSource", function(arg0)
    local DataTable = {
        {
            models = {
                buttonText = "Zombies",
                disabled = true
            },  
            properties = {
                section = "zm"
            }
        },
        { --I've added an extra element entry here to demonstrate how you'd add another element to the data table.
            models = {
                buttonText = "Multiplayer",
                disabled = false
            },  
            properties = {
                section = "mp"
            }
        }
    }

    return DataTable
end, true)
```

That's it. The data table gets parsed by the `ListSetup` function, and creates a data source from that which you've now attached to the `DataSources` object.

## Setting up a list item element

There isn't much different in the setup of a normal widget versus a widget you're going to use under a UIList. However, do note the following points:
* Make sure your element is added as a `require()` in the menu/widget your `UIList` has been made in, and add it to your zone. You'd be surprised how much you may forget to do this!
* Set your element's class using `Elem:setClass()`, e.g. `Elem:setClass(CoD.SectionListButton)`.
* Use the examples set out in the explanations for data table models & properties accordingly to your requirement for making your element differ on a per-entry basis.

## Finished

This should be all you need to setup a basic data source & `UIList`. You can from here go to a more advanced level, and set up button callbacks, button states, etc. There are plenty of examples of this available if you use JariK's LuaDecompiler to decompile Black Ops III LUA files. List buttons may also be covered in a future, separate, guide.
