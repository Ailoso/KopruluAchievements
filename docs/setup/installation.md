---
layout: page
title: Installation
subtitle: Getting Started
menubar: docs_menu
show_sidebar: false
toc: false
---

## Add the Extension to Your Map/Mod

To facilitate future updates and version migration the data is not added into the mod but instead it is added to your map or core Mod, so some slight modification is still required.

To begin [Download](https://github.com/Ailoso/KopruluAchievements) the latest release of the Libraries and extract it.

Place the folder `KopruluAchievements.SC2Mod` in the Starcraft 2 Installation Folder > Mods, you may rename the mod if you need to keep the previous named extension.

Open your Core Mod file or your Map file, Navigate to the `Top Left Menu > File > Dependencies` and Add the Koprulu Achievements mod file into it.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/JjvWFTyl.png" alt="Example image" large_link="https://i.imgur.com/JjvWFTy.png" %}

Dependencies List
</div>
<div class="column is-6">
</div>
</div>

Finally to test that the mod is working properly, add the following during your Map Initialization `Initialize Achievements`, Then Launch the map and press F9, the Menu will act as default for now and will require some more UI tweaks to be fully complete.

Now you've finished adding the mod to your Map/Mod please proceed and follow the [Configuration](/KopruluAchievements/docs/setup/configuration/) step next.