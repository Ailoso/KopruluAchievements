---
layout: page
title: Data Backup
subtitle: New Version Update
menubar: docs_menu
show_sidebar: false
toc: true
---

## Where to Start?

Before starting, download the Latest Version but do not delete your old version as any personalized data will be saved before removing the old Mod. Place the old version somewhere safe as an additional safety later.

## Creator Variables
Similar to the initial setup all Creator variable values must be noted down in order to set them later.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/yoV0K3gl.png" alt="Example image" large_link="https://i.imgur.com/yoV0K3g.png" %}

Target Folder
</div>
<div class="column is-6">
</div>
</div>

## Unpack as Components

In order to quickly acess any other files it's easier to unpack as components, this can be done by Opening the Mod, heading to the top bar under `File > Save As...`, then naming it differently than your current mod and just below the file name set the file type to `Starcraft II Components Folder`, this will let us navigate the Mod file as a set of folders to simply later copy paste our required files.

## Dev Panels File

This file contains your customized UI including but not limited to: Any modified Tabs for the Tree View

Next is saving the DevPanels file which can be found in the `Components Folder of the Mod > Base.SC2Data > UI > Layout > KL_DevPanels.SC2Layout` Copy this file and save it somewhere else, you'll need it for later.

## Achievement User Data

Achievement Data is already contained in your main Mod/Map so it won't be needed to Backup any of it.

If you're upgrading from `V1.0` remove any fields referencing Race as they're no longer needed being replaced by the `Set Toast Style` Action.

```XML
    <GameLink GameLink="Zerg">
        <Field Id="Race"/>
    </GameLink>
```

`Note:` User data should always be contained within your main Mod or Map other than the achievements Mod, if for any reason this is not the case the Instructions below should help solve it.

If achievement Data is in the Achievements mod go to the `Components Folder > Base.SC2Data > GameData > UserData.xml` copy this file and save it for later