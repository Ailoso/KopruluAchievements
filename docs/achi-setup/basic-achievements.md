---
layout: page
title: Basic Achievements
subtitle: Achievement Setup
menubar: docs_menu
show_sidebar: false
toc: true
---

## Intro

Achievement Data is added by adding an Instances in the `Koprulu - Achievements` UserType in your core Mod or Map's Data, ideally it should be contained in a mod or if there is a single Map in your game it can remain in the Map itself, this is to facilitate Updates without requiring to Migrate data from the `KopruluAchievements` Mod.

Libraries handle Display and Order by themselves only requiring the Data to be added properly.

## Finding the User Types

Start by Launching the Data Module, to find the User Types click on the green `+` sign at the left of the Tabs > Edit Advanced Game Data > User Types

Optionally you can Toggle the Detail View on the top to make reading the Instances easier

In here you will find the user called `Koprulu - Achievements`, click it and now you should be able to view on the right side panel a field called Instances

**DO NOT Modify the Fields, Name or Suffix**

From here you may press the Add Button to Add a new Achievement Instance.

## Adding Achievement Data

Press the Add button in the Instances box, or Right Click > Add to begin.

Starting Top to Bottom we start configuring, you may ignore any properties not listed in this section.

* **Id:** Sitting at the top of the list, a short identifiable name that you will be using when awarding your Achievement, it is not visible to the User

* **Category:** This Integer should match with your Listbox ID, attempting to go over the amount of available Listboxes will cause errors.
* **Description:** A concise Description of the Requirements of your Achievement, this is readable to the User from the User Profile and Toast
* **Icon:** The Achievement's Icon image, for optimal Quality a 112x112 image is recommended, only the image value is required
* **ID:** This ID is what is saved to player's Banks, Less than 10 characters are recommended with no Special Characters
* **Points:** The Amount of points gained from earning the Achievement, if the value is set to 0 it will become a hidden Feat of Strength
* **Race:** This property is what sets the Race style of the Achievement Toast, it has no effect on anything else
* **Title:** The name of your Achievement, only rule is to not make it overflow out of the frame, does not support double lines

The display order is dictated by the order from top to bottom, though it does not matter if there are achievements from different categories mixed together.

The "Expanded Content" feature can be seen when a + sign is displayed in an achievement, this "Content" means it can be clicked and expanded to view additional info such as Series, Criteria, Progress and Rewards, how these are set can be seen in their respective Sections.

You may view related Fuctions or Actions for Basic Achievements