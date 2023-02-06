---
layout: page
title: Actions
subtitle: Helper Actions
menubar: docs_menu
show_sidebar: false
toc: true
---

## What are they for?

The Achievement Libraries contain a number of Custom Actions used by Developers in order to Award, Add Progress and in general Interact with the User Profile Menu.

They are as follows:

## Initialize Achievements

`Required` to be placed a single time at Map Initialization, this action has no parameters and will ignore AI players and empty slots.

## Set Toast Style

This action sets the Achievement Toast Style per player, `Required` to be placed at least once During Map Intialization or after if the style is different than Terran.

By default the style is set to Terran.

This actions takes in a `Race` Paramter as well as a `Player` Parameter, currently only `Terran, Zerg and Protoss` Styles are available

## Show User Profile

This action can be used to open the User Profile as part of a custom button or game action, while in SinglePlayer the menu will pause the game until closed.

**Grammar**

Show User Profile for Player `Player`.

It is only required to set a triggering `Player` for this action.

## Award Achievement

Used to Award any regular achievement, this action will take care of saving to Banks, Displaying a Toast and Updating the User Profile accordingly. Once an achievement is awarded it will be displayed in the Recent Achievements list along with the completion Date.

**Grammar**
Award Achievement `Achievement` (`Player`)

The two Parameters used in this action are for an `Achievement` Instance Value and awarding `Player`.

## Update Achievement Progress

This action should be used for any and all types of Achievements using a `Progress Bar` having a required count higher than 0.

When updating a series it is required that only the first Achievement in the Series is updated, the rest will be handled by the internal libraries, doing otherwise will result in an error.

No Award Achievement action is required as once the player reaches the desired Progress the achievement will be `Awarded` by itself.

**Grammar**

Update `Achievement` Progress Add (`ValueIncrease`) for Player `Player` and Save to Bank `SavetoBank`

This action requires an `Achievement` Instance, the Amount of Progress added set by `ValueIncrease`, a triggering `Player` and the Option `SavetoBank`

When using the `SavetoBank` there are two options when Updating a Series, `True` or `False`. This means Setting the value to `False` will only store the progress Locally without it going permanently into a bank, deleting the progress if the player leaves the level without completing it. Or Setting it `True` resulting in saving each progress point to the Bank permanently, keeping progress persistently.