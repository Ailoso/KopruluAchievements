# Koprulu Achievements
By the community, for the community.

Achievements Beta 1
Currently Supports:
- Achievement Awarding Animations
- Achievement Race Styles
- Blizz-like Achievement Display
- Automatic data fetching and sorting
- Support for up two 8 players
- Recently Earned Achievement Display

## How to Use the Libraries
A new action "Award Achievement" will handle giving the player an achievement from UserTypes, bank saving and animation display.
The function "Player Has Achievement" will allow the developer to check whether a player has earned or not a particular achievement
The function "Return Player Bank" will allow the dev to get the bank of a specific player by using his integer index

## How to Add the Mod
Feel free to ask any questions, request features or come say hi at https://discord.gg/45kseu or Chonky Kat#8186

###### Adding it to your map
1. Add mod as dependency by going to File>Dependencies and finding the mod in your folder
2. Add your desired Bank name to the preload list by going to Map>Preload Info and adding your bank name within the banks tab
3. The scrip will handle achievement initialization and bank loads

###### Customizing the libraries

1. Modifying the Bank Name
By default the libraries use the name KLClassic but it can be easily changed within the mod by finding the constant variable "KL_AchievementSectionConstant" which can be located here.

![Constant Location](https://i.imgur.com/yQwOoID.png)

2. Adding new Achievements
New achievements can be added inside user types on a pre-existing template. You can find it in Data> User Types> Koprulu Achievements
The minimum required fields are:
- Category: the number has to match the number of buttons in the user Tree View
- Description
- Icon
- ID: can be a combination of numbers and letters
- Points
- Race: It will determine display style
- Title
The remaning fields are not in use at the moment.
Achievements can be added in any order, but any that must be above a particular achievement within a category must be higher in the list.

3. Adding new Achievement Categories
Sample buttons are added by default but it can be customized to turn them into either normal or collapsible buttons according to your needs. Some text editing is required but once set up it will be mostly permanent, even through updates.

![Tree View](https://i.imgur.com/0CB0a5B.png)
(The TreeView)

Within the mod folder you will find a UI file that must be edited in order to add new achievement sections. Currently 5 max tabs are supported but more will be added down the line. By navigating within the mod components folder to Base.SC2Data/UI/Layout/KL_DevPanels.SC2Layout you will find the required templates in order to modify existing buttons and categories.

Category Names
```XML
    <!-- Custom Name displays for Tab Buttons -->
    <Constant name="Tab0Name" val="Profile Summary"/>
    <Constant name="Tab1Name" val="Insurrection"/>
    <Constant name="Tab2Name" val="Terran"/>
    <Constant name="Tab3Name" val="Zerg"/>
    <Constant name="Tab4Name" val="Protoss"/>
    <Constant name="Tab5Name" val="Feats of Strength"/>
```
by editing the "val=" you can change the display name

If a Tab is to be turned into a collapsible tab four elements must be modified
1. The button itself
2. The Container below the button
3. The buttons inside the container
4. Required Animations

in order to turn a normal button into a collapsible one the template must be modified.

Normal
```XML
            <Frame type="Button" name="TabButton0" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
```
Collapsible
```XML
            <Frame type="Button" name="TabButton1" template="KL_UserProfileTemplates/VerticalTabArrowButtonTemplate">
```
A frame Below must be added called SubTabGroup{NumberofSubGroups} with at least one button inside it and it's "Bottom" anchor set to the name of the last button in the list

```XML
            <Frame type="Frame" name="SubtabGroup1">
                <!-- Check that anchor is the Parent Tab -->
                <Anchor side="Top" relative="$parent/TabButton1" pos="Max" offset="0"/>
                <!-- Modify anchor to the last tab added on the panel -->
                <Anchor side="Bottom" relative="$this/SubTabButton0" pos="Max" offset="0"/>
                <Anchor side="Left" relative="$parent" pos="Min" offset="20"/>
                <Anchor side="Right" relative="$parent" pos="Max" offset="0"/>

                <CollapseLayout val="True"/>
                <Constant name="SubTabWidth" val="321"/>
                <Visible val="False"/>

                <!-- Add Tabs from this point onward -->

                <!--
                ============================
                Collapsible Sub Tab Template
                ============================
                
                Creates a Tab with subtabs inside
                -->

                <Frame type="Button" name="SubTabButton0" template="KL_UserProfileTemplates/VerticalTabButtonTemplate">
                    <Anchor side="Top" relative="$parent" pos="Min" offset="0"/>
                    <Anchor side="Left" relative="$parent" pos="Min" offset="0"/>

                    <Width val="#SubTabWidth"/>
                    <Handle val="SubTab00"/>
    
                    <Frame type="Label" name="Label">
                        <Text val="#Tab2Name"/>
                    </Frame>
                </Frame>
            </Frame>
```

next is the animations and state group

within the stategroup "TabToggles" the following must be added, the number of SubTab States must increase with each SubTab button in the list
```XML
            <State name="Tab01">
                <Action type="SetProperty" frame="$Tab01" Toggled="True"/>
                <Action type="SetState" frame="$Tab01" group="ExpansionState" state="Expanded"/>
                <Action type="SetProperty" frame="$Listbox01" Visible="True"/>
            </State>

            <State name="Tab01Off">
                <Action type="SetProperty" frame="$Tab01" Toggled="True"/>
                <Action type="SetState" frame="$Tab01" group="ExpansionState" state="Collapsed"/>
                <Action type="SetProperty" frame="$Listbox01" Visible="True"/>
            </State>

            <State name="Sub01Tab00">
                <Action type="SetState" frame="$Tab01" group="ExpansionState" state="Expanded"/>
                <Action type="SetProperty" frame="$SubTab00" Toggled="True"/>
                <Action type="SetProperty" frame="$Listbox02" Visible="True"/>
            </State>
```

The following animations are required for a Sub Tab, SubTab animations must be added for each new SubTab button.
```XML
        <Animation name="Tab01Toggle">
            <Event event="OnClick" action="Reset,Play" frame="$Tab01"/>
    
            <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
                <Key type="Identifier" time="0.0" value="Tab01"/>
            </Controller>
        </Animation>
    
        <Animation name="Tab01ToggleOff">
            <Event event="OnClick" action="Reset,Play" frame="$Tab01/UntoggleButton"/>
    
            <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
                <Key type="Identifier" time="0.0" value="Tab01Off"/>
            </Controller>
        </Animation>
    
        <Animation name="Sub01Tab00Toggle">
            <Event event="OnClick" action="Reset,Play" frame="$SubTab00"/>
    
            <Controller type="State" end="Pause" frame="$this" stateGroup="TabToggles">
                <Key type="Identifier" time="0.0" value="Sub01Tab00"/>
            </Controller>
        </Animation>
```

Lastly the "Summary" State within the "TabToggles" must get a new line added per each button that opens a new SubTab
```XML
                <!-- Any Parents of Subtabs should be toggled Off when pressing the Summary Button -->
                <Action type="SetProperty" frame="$Tab01" Toggled="False"/>
```
