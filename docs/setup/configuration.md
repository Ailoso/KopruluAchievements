---
layout: page
title: Installation
subtitle: Getting Started
menubar: docs_menu
show_sidebar: false
toc: true
---

## Setting up Values

Next is configuring the default variables that control several aspects of the libraries, these values should be updated with each new release.

Start by opening the `KopruluAchievements` folder and launching the `ComponentList.SC2Components` file to open the mod.

Navigate to the folder `Creator Only > Variables` in here you will find the variables you need to modify.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/yoV0K3gl.png" alt="Example image" large_link="https://i.imgur.com/yoV0K3g.png" %}

Target Folder
</div>
<div class="column is-6">
</div>
</div>

Go to `KL_AchievementNameConstant` and set it to the name of your Bank file. 

Go to `KL_AchievementSectionConstant` and set to the name of the Section in which achievements wil be stored

Go to `KL_MaxPlayers` and set to the number of players in your game, including AI.

Go to `KL_MaxAvailableLists` and set it to the number of categories you're gonna use.

These values are important for optimization purposes.

## Add Preload Info

If you have not yet set a Preload Info in your Mod/Map you can add it at this point by heading to the `Top Bar > Mod > Preload Info` or `Top Bar > Map > Preload Info` depending on your case.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/5AyWGksl.png" alt="Example image" large_link="https://i.imgur.com/5AyWGks.png" %}
Preload Info Menu
</div>
<div class="column is-6">
</div>
</div>

In this window you may select the pre-existing value and set the name to the Name of your Bank used in the `KL_AchievementNameConstant`

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/5AyWGksl.png" alt="Example image" large_link="https://i.imgur.com/5AyWGks.png" %}
Preload Info Window
</div>
<div class="column is-6">
</div>
</div>

## Adding Additional Lists

By default only `X` Achievement lists are available, the number of lists has to match with the number of lists in the `KL_MaxAvailableLists`.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/5AyWGksl.png" alt="Example image" large_link="https://i.imgur.com/5AyWGks.png" %}
List Example
</div>
<div class="column is-6">
</div>
</div>

At this point you may receive some UI errors and only the default lists may display, but don't worry we'll continue on [UI Modification](/KopruluAchievements/docs/setup/ui-changes/)