---
layout: page
title: Basic Achievements
subtitle: Achievement Setup
menubar: docs_menu
show_sidebar: false
toc: true
---

## What are They?

Series Achievements are linked achievements that have a progressive goal, they occupy the same slot in the List but display within their Expanded Content section their different unlockable Tiers, whenever one is completed the next one in the series occupies the main slot until the entire Series is complete. The Points from each achievement in the series are added up. 

Up to 10 Achievements may be part of a series, including the Main Item.

They can combine with Several other types of Achievements with different behaviors.

## Adding a Series Achievement

Series require some additional settings for the main item and the following ones do the following to add your own series: 

1. Create Basic Achievements for each item without any additional settings.
2. On the Main Item head to the `Series` Value and add each Achievement in order, It is required for the main item to be added on the first Index of the List.
3. On all other Items head to the `IsPartOfSeries` value and type in `True`.

Now you should be able to click the achievement and in the Expanded Content section be able to see your achievements in the Series.

Feat of Strength Series can be made by setting the points of the achievements to 0. `(This feature may be buggy at Release 1.0)`.

## Series + Progress

When combining a Series Achievement and a Progress type only the first item needs to be updated and achievements are awarded automatically as the Requirements are met. Additionally above the progress bar, the name of the Next Achievement in the Series is displayed.

The same way a Progress Achievement is made applies here by setting the `RequiredCount` value above 0, The progress is the same across all achievements meaning the progress of the last counts towards the next.

You may view related Fuctions or Actions for Series Achievements.