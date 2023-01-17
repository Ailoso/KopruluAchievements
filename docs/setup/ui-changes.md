---
layout: page
title: UI Changes
subtitle: Getting Started
menubar: docs_menu
show_sidebar: false
toc: true
---

## Listbox Setup

Some basic Layouts knowledge is required for this part.

Listboxes are containers housing individual Achievement Items, the number next to their name corresponds to the ID used when placing achievement in their containers.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/yoV0K3gl.png" alt="Example image" large_link="https://i.imgur.com/yoV0K3g.png" %}

Listbox Sample
</div>
<div class="column is-6">
</div>
</div>

Open the KopruluAchievements.SC2Mod Folder and using a text editor (preferably VSC along with the SC2Layout plugin, link tutorial here).
Navigate to the folder `Base.SC2Data > UI > Layout` in here open the file `KL_DevPanels.SC2Layout`.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/yoV0K3gl.png" alt="Example image" large_link="https://i.imgur.com/yoV0K3g.png" %}

Target Folder
</div>
<div class="column is-6">
</div>
</div>

Find the section labeled `User Profile Achievement Listboxes`, under it there’s a frame called `DevAchievementsListboxContainerTemplate` containing a sample of 4 active listboxes, if more were required simply copy paste one of the frames under it and increase the number.
The Handle Property must also have it’s value increased

```XML
    <Frame type="Frame" name="AchievementListbox5" template="KL_AchievementListboxTemplate/AchievementsListBoxTemplate">
        <Handle val="Listbox05"/>
    </Frame>
```
If one must be removed, make sure to update the number of Listboxes in the Variables from the previous section are also updated.

## Tree View List Button

The Tree View buttons are the buttons on the left side panel that correspond to each listbox's display and can support one submenu. 
There are two types of Tree View Buttons available:
* Tab Buttons
    - These buttons act as a normal radio button.
* Arrow Tab Buttons
    - These buttons can have a Submenu Attached below them indicated by the Arrow on it's right side.

`TabButton0` should never be removed
To edit the placement first find the file `KL_DevPanels.SC2Layout` in the section labeled `User Profile Tree View`, under it there's a frame called `DevScrollableFrameTemplate` Containing everything related to the Tree View

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/yoV0K3gl.png" alt="Example image" large_link="https://i.imgur.com/yoV0K3g.png" %}

Tree View Sample
</div>
<div class="column is-6">
</div>
</div>

###### Adding a Regular Tab Button

Adding a new button to the list consists of the following steps

1. Copy the Template code from below and paste it after the last TabButton. Replace the name and Handle 
```XML
    <Frame type="Button" name="TabButton1" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
        
        <Handle val="Tab1"/>

        <Frame type="Label" name="Label">
            <Text val="@UI/ScreenUserProfile/Category1TabLabel"/>
        </Frame>
    </Frame>
```

2. Make sure a regular button is always using the Template `KL_UserProfileTemplates/VerticalTabButtonTemplate`
3. If the previous frame was a SubTabGroup anchor your new button to the bottom of the list using `<Anchor side="Top" relative="$parent/SubtabGroup1" pos="Max" offset="0"/>`, replacng the name with the name of the last list. Otherwise skip this step.
eg:
```XML
    <Frame type="Button" name="TabButton3" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
        <Anchor side="Top" relative="$parent/SubtabGroup1" pos="Max" offset="0"/>

        <Handle val="Tab3"/>

        <Frame type="Label" name="Label">
            <Text val="@UI/ScreenUserProfile/Category3TabLabel"/>
        </Frame>
    </Frame>
```
At this point disregard the Text label as that will be seen and modified later during the Localization steps.

###### Adding a Tab Arrow Button

These buttons contain submenus and adding one consists of a few more steps

1. Copy the Template code from below and paste it after the last TabButton. Replace the name and Handle 

```XML
    <Frame type="Button" name="TabButton2" template="KL_UserProfileTemplates/VerticalTabArrowButtonTemplate">

        <Handle val="Tab2"/>

        <Frame type="Label" name="Label">
            <Text val="@UI/ScreenUserProfile/Category2TabLabel"/>
        </Frame>
    </Frame>
```
2. Make sure an Arrow Tab button is always using the Template `KL_UserProfileTemplates/VerticalTabArrowButtonTemplate`
3. Apply the same Anchor rules as with the regular Tab Buttons, If the previous frame was a SubTabGroup anchor your new button to the bottom of the list using `<Anchor side="Top" relative="$parent/SubtabGroup1" pos="Max" offset="0"/>`, replacng the name with the name of the last list. Otherwise skip this step.
4. Add the following after the Label
```XML
    <StateGroup name="ExpansionState">
        <State name="Expanded">
            <Action type="SetProperty" frame="$parent/SubtabGroup1" visible="True"/>
        </State>
    </StateGroup>
```
This state requires no events and controls the visibility of the SubTabGroup it is attached to, set the name to the number of Subtab Groups you have, you will have to later match this name, your code should now look similar to this.

```XML
    <Frame type="Button" name="TabButton2" template="KL_UserProfileTemplates/VerticalTabArrowButtonTemplate">

        <Handle val="Tab2"/>

        <Frame type="Label" name="Label">
            <Text val="@UI/ScreenUserProfile/Category2TabLabel"/>
        </Frame>

        <StateGroup name="ExpansionState">
            <State name="Expanded">
                <Action type="SetProperty" frame="$parent/SubtabGroup1" visible="True"/>
            </State>
        </StateGroup>
    </Frame>
```

Next is adding a submenu under your new Arrow Tab Button by doing the following.

1. Copy this template below
```XML
    <Frame type="Frame" name="SubTabGroup1" template="KL_DevPanels/SubtabGroupTemplate">
        <Anchor side="Top" relative="$parent/TabButton2" pos="Max" offset="0"/>
    </Frame>
```
2. Set the Top anchor to your last Arrow Tab Button using `<Anchor side="Top" relative="$parent/TabButton2" pos="Max" offset="0"/>`
3. Place SubTab Buttons by copy pasting the following, set a name starting from 0 and set the width to `<Width val="#SubTabWidth"/>`
```XML
    <Frame type="Button" name="SubTabButton0" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
        <Anchor side="Top" relative="$parent" pos="Min" offset="0"/>
        <Anchor side="Right" relative="$parent/$parent/$parent/ScrollBarBackground" pos="Min" offset="-5"/>

        <Width val="#SubTabWidth"/>
        <Handle val="SubTab00"/>

        <Frame type="Label" name="Label">
            <Text val="@UI/ScreenUserProfile/Category3TabLabel"/>
        </Frame>
    </Frame>
```
4. On the first button use `<Anchor side="Top" relative="$parent" pos="Min" offset="0"/>` any buttons after do not require the Top Anchor eg:
```XML
    <Frame type="Button" name="SubTabButton1" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
        <Anchor side="Right" relative="$parent/$parent/$parent/ScrollBarBackground" pos="Min" offset="-5"/>
        
        <Width val="#SubTabWidth"/>
        <Handle val="SubTab01"/>

        <Frame type="Label" name="Label">
            <Text val="@UI/ScreenUserProfile/Category4TabLabel"/>
        </Frame>
    </Frame>
```
5. Finally back at your SubTabGroup add a bottom anchor set to the bottom of your last SubTabButton, your code should look like this
```XML
    <Frame type="Frame" name="SubtabGroup1" template="KL_DevPanels/SubtabGroupTemplate">
        <Anchor side="Top" relative="$parent/TabButton2" pos="Max" offset="0"/>
        <Anchor side="Bottom" relative="$this/SubTabButton1" pos="Max" offset="0"/>

        <!-- Add Tabs from this point onward -->

        <Frame type="Button" name="SubTabButton0" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
            <Anchor side="Top" relative="$parent" pos="Min" offset="0"/>
            <Anchor side="Right" relative="$parent/$parent/$parent/ScrollBarBackground" pos="Min" offset="-5"/>

            <Width val="#SubTabWidth"/>
            <Handle val="SubTab00"/>

            <Frame type="Label" name="Label">
                <Text val="@UI/ScreenUserProfile/Category3TabLabel"/>
            </Frame>
        </Frame>

        <Frame type="Button" name="SubTabButton1" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
            <Anchor side="Right" relative="$parent/$parent/$parent/ScrollBarBackground" pos="Min" offset="-5"/>
            
            <Width val="#SubTabWidth"/>
            <Handle val="SubTab01"/>

            <Frame type="Label" name="Label">
                <Text val="@UI/ScreenUserProfile/Category4TabLabel"/>
            </Frame>
        </Frame>
    </Frame>
```

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/yoV0K3gl.png" alt="Example image" large_link="https://i.imgur.com/yoV0K3g.png" %}

End Result
</div>
<div class="column is-6">
</div>
</div>

Now you should be able to launch a map, access the menu by pressing F11 and view your progress, next Achievements are getting added to display something. [Installation](/KopruluAchievements/docs/setup/installation/)