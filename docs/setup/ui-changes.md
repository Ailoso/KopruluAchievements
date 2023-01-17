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

They are composed of a Container Frame featuring a ScrollBar that becomes active once there's more than 5 Items and a Frame counting the total earned and earnable points, these are counted automatically by the libraries and require no additional setup.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/XkIG6sml.png" alt="Example image" large_link="https://i.imgur.com/XkIG6sm.png" %}

Listbox Sample
</div>
<div class="column is-6">
</div>
</div>

Open the KopruluAchievements.SC2Mod Folder and using a text editor (preferably VSC along with the SC2Layout plugin, link tutorial here).
Navigate to the folder `Base.SC2Data > UI > Layout` in here open the file `KL_DevPanels.SC2Layout`.

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/VPV1zmKl.png" alt="Example image" large_link="https://i.imgur.com/VPV1zmK.png" %}

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

`TabButton0` should never be removed.

To edit the placement first find the file `KL_DevPanels.SC2Layout` in the section labeled `User Profile Tree View`, under it there's a frame called `DevScrollableFrameTemplate` Containing everything related to the Tree View

<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/QEX0AEml.png" alt="Example image" large_link="https://i.imgur.com/QEX0AEm.png" %}

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

## Modifying Display StateGroups

Since the game is paused while the Achievements menu is open, no trigger events can be used, thus the libraries rely on Animations and Stategroups to handle Navigation through it's menus, now we have to modify and add new animations to display our brand new buttons.

###### Summary Tab

First navigate witin the `KL_DevPanels.SC2Layout` file under a section labeled `Tab States`, until you find the `TabToggles` Stategroup, this State is responsible from Toggling Tab buttons and Collapsible Tabs off when selecting the summary.

We'll start modifying the Summary State after the Comment we'll be adding an action per each TabArrowButton in our case:
```XML
    <!-- Any Parents of Subtabs should be toggled Off when pressing the Summary Button -->
    <Action type="SetProperty" frame="$Tab2" Toggled="False"/>
```

###### Regular Tab Buttons

These tabs are controlled by a single state and only require an event and an action, copy paste the following for your regular Tabs placing it after the Summary State

```XML
    <State name="Tab01">
        <Action type="SetProperty" frame="$Tab1" Toggled="True"/>
        <Action type="SetProperty" frame="$Listbox01" Visible="True"/>
    </State>
```

Once again naming is important as these states are toggled as well by some animations down the line

###### Arrow Tab Buttons

These Tabs require two states as they remain toggled even when de-selected as long as you're browsing an item inside the category.

```XML
    <State name="Tab02">
        <Action type="SetProperty" frame="$Tab2" Toggled="True"/>
        <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Expanded"/>
        <Action type="SetProperty" frame="$Listbox02" Visible="True"/>
    </State>

    <State name="Tab02Off">
        <Action type="SetProperty" frame="$Tab2" Toggled="True"/>
        <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Collapsed"/>
        <Action type="SetProperty" frame="$Listbox02" Visible="True"/>
    </State>
```

SubTabs come after the Arrow Tab States and look quite similar to a regular tab with an extra property, copy paste the following for your SubTabs

```XML
    <State name="Sub02Tab00">
        <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Expanded"/>
        <Action type="SetProperty" frame="$SubTab00" Toggled="True"/>
        <Action type="SetProperty" frame="$Listbox03" Visible="True"/>
    </State>

    <State name="Sub02Tab01">
        <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Expanded"/>
        <Action type="SetProperty" frame="$SubTab01" Toggled="True"/>
        <Action type="SetProperty" frame="$Listbox04" Visible="True"/>
    </State>
```

With this our Stategroup should look like the following.

```XML
    <StateGroup name="TabToggles">
        <DefaultState val="Summary"/>
    
        <State name="Summary">
            <Action type="SetProperty" frame="$SummaryTab" Toggled="True"/>
            <Action type="SetProperty" frame="$parent/$parent/RecentAchievementsListBox" Visible="True"/>
            
            <Action type="SetProperty" frame="$parent/$parent/LastMatchPanel" Visible="True"/>
            <Action type="SetProperty" frame="$parent/$parent/MatchStoryPanel" Visible="True"/>

            <!-- Any Parents of Subtabs should be toggled Off when pressing the Summary Button -->
            <Action type="SetProperty" frame="$Tab2" Toggled="False"/>
        </State>

        <State name="Tab01">
            <Action type="SetProperty" frame="$Tab1" Toggled="True"/>
            <Action type="SetProperty" frame="$Listbox01" Visible="True"/>
        </State>

        <State name="Tab02">
            <Action type="SetProperty" frame="$Tab2" Toggled="True"/>
            <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Expanded"/>
            <Action type="SetProperty" frame="$Listbox02" Visible="True"/>
        </State>

        <State name="Tab02Off">
            <Action type="SetProperty" frame="$Tab2" Toggled="True"/>
            <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Collapsed"/>
            <Action type="SetProperty" frame="$Listbox02" Visible="True"/>
        </State>

        <State name="Sub02Tab00">
            <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Expanded"/>
            <Action type="SetProperty" frame="$SubTab00" Toggled="True"/>
            <Action type="SetProperty" frame="$Listbox03" Visible="True"/>
        </State>

        <State name="Sub02Tab01">
            <Action type="SetState" frame="$Tab2" group="ExpansionState" state="Expanded"/>
            <Action type="SetProperty" frame="$SubTab01" Toggled="True"/>
            <Action type="SetProperty" frame="$Listbox04" Visible="True"/>
        </State>
    </StateGroup>
```

## Modifying Toggle Animations

The following animations control the behavior of the Tab Buttons and activate some of the States, they can be found under the label `Tab Animation States`

###### Regular Tab Animation

These do not require an On/Off Animation same as it's stategroup, set the frame on the event to your Tab's Handle and the Identifier' Value in the Key to the name of it's corresponding StateGroup

```XML
    <Animation name="Tab01Toggle">
        <Event event="OnClick" action="Reset,Play" frame="$Tab1"/>
    
        <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
            <Key type="Identifier" time="0.0" value="Tab01"/>
        </Controller>
    </Animation>
```

###### Arrow Tab Animation

Same as it's StateGroup counterpart these require an animation to activate the StateGroups, same as before set the frame on the event to your Tab's Handle and the Identifier' Value in the Key to the name of it's corresponding StateGroup the only difference poiting the `ToggleOff` animation to `frame="$Tab2/UntoggleButton"`

```XML
    <Animation name="Tab02Toggle">
        <Event event="OnClick" action="Reset,Play" frame="$Tab2"/>

        <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
            <Key type="Identifier" time="0.0" value="Tab02"/>
        </Controller>
    </Animation>

    <Animation name="Tab02ToggleOff">
        <Event event="OnClick" action="Reset,Play" frame="$Tab2/UntoggleButton"/>

        <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
            <Key type="Identifier" time="0.0" value="Tab02Off"/>
        </Controller>
    </Animation>
```

SubTab animations come right after just like before

```XML
    <Animation name="Sub02Tab00Toggle">
        <Event event="OnClick" action="Reset,Play" frame="$SubTab00"/>

        <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
            <Key type="Identifier" time="0.0" value="Sub02Tab00"/>
        </Controller>
    </Animation>

    <Animation name="Sub02Tab01Toggle">
        <Event event="OnClick" action="Reset,Play" frame="$SubTab01"/>

        <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
            <Key type="Identifier" time="0.0" value="Sub02Tab01"/>
        </Controller>
    </Animation>
```

Every part of this tutorial is in the `KL_DevPanels.SC2Layout` file contained in the Sample Achievements Map


<div class="columns">
<div class="column is-6">
{% include image-modal.html ratio="is-16by9" link="https://i.imgur.com/HO0ykAWl.png" alt="Example image" large_link="https://i.imgur.com/HO0ykAW.png" %}

End Result
</div>
<div class="column is-6">
</div>
</div>


Now you should be able to launch a map, access the menu by pressing F9 and view your progress, next Achievements are getting added to display something inside the Listboxes. [Adding Basic Achievements](/KopruluAchievements/docs/achi-setup/basic-achievements/)