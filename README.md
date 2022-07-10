# Koprulu Achievements
By the community, for the community.

Achievement libraries for Starcraft 2 Custom Maps that work completely independant from Starcraft 2 Achievements.

Achievements Beta 0.4 (24-10-2021)
Currently Supports:
- Achievement Awarding Animations
- Achievement Race Styles
- Blizz-like Achievement Display
- Automatic data fetching and sorting
- Support for up to 8 players
- Recently Earned Achievement Display
- Custom Button in the Game Menu, Hotkey (F11)
- Stat and Last Match Displays
- Game Pause

## Screenshots
* Some screenshots were taken during the Development of UED:First Light.

![Achievement Toast Styles](https://i.imgur.com/Y4gdvIJ.png)
Animated Achievement toasts come supported in all 3 Race styles

![Achievement Button](https://i.imgur.com/rVLP2So.png)
A new battle menu button is supported along with a custom hotkey. Supports all standard SC2 Console Skins

![Recent Achievements](https://i.imgur.com/cLv1TLT.png)
A list in the profile summary comes with a fully working recent achievements list, a tooltip is supported to show the achievement's info.

![Achievements Lists](https://i.imgur.com/ExAEG1g.png)
Achievements lists autofill from the Achievement Data in User types, the order is determined by the addition order, supports up to 20 Achievements in a single list.

![Tab Tree View](https://i.imgur.com/TkzwOQV.png)
A custom tab tree view UI is used to allow for tabs and subtabs to house all your achievement categories, list autoscales with a scrollbar to fit more categories.

## How to Use the Libraries
A new action "Award Achievement" will handle giving the player an achievement from UserTypes, bank saving and animation display.

The function "Player Has Achievement" will allow the developer to check whether a player has earned or not a particular achievement.

The function "Return Player Bank" will allow the dev to get the bank of a specific player by using his integer index.

In-game a new button in the Menu bar can be used to open the Panel but the hotkey (F11) can also be used



## How to Install the Mod
Feel free to ask any questions, request features or come say hi at https://discord.gg/45kseu or Chonky Kat#8186

###### Adding it to your map/Mod
1. Add mod as dependency by going to File>Dependencies and finding the mod in your folder
2. Add your desired Bank name to the preload list by going to Map/Mod>Preload Info and adding your bank name within the banks tab
3. The script will handle achievement initialization and bank loads, in the case of the trigger not working the action "Initialize Achievements" must be added to the map initalization

###### Customizing the libraries

1. Modifying the Bank Name
By default the libraries use the name KLClassic but it can be easily changed within the mod by finding the constant variable "KL_AchievementNameConstant" which can be located here. There are more instances of "KLClassic" which have to be replaced with your bank name.

![Constant Location](https://i.imgur.com/C1FMHXA.png)

The variabe "KL_AchievementSectionConstant" will be the name of the section where all achievements are stored.
If you are already using a bank for your map/mod the variable name "KL_AchievementNameConstant" has to match with your bank name. as well as replacing all instances of KLClassic with your bank name

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

### It's recommended that achievements are added in your main mod or map, instead of the achievements mod.

3. Adding new Achievement Categories
Sample buttons are added by default but it can be customized to turn them into either normal or collapsible buttons according to your needs. Some text editing is required but once set up it will be mostly permanent, even through updates.

![Tree View](https://i.imgur.com/0CB0a5B.png)
(The TreeView)

Within the mod folder you will find a UI file that must be edited in order to add new achievement sections. Currently 9 max tabs are supported but more will be added down the line. By navigating within the mod components folder to Base.SC2Data/UI/Layout/KL_DevPanels.SC2Layout you will find the required templates in order to modify existing buttons and categories.

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

Customizable text is found as a UI file named KL_LocalizedText.SC2Layout, by default these are the texts contained, but can be set to any other text by the developer, the layouts for the Stats panel and Last Match panel are not yet Customizable
```XML
    <!-- Custom Name displays for Tab Buttons -->
    <Constant name="Tab0Name" val="Profile Summary"/>
    <Constant name="Tab1Name" val="Insurrection"/>
    <Constant name="Tab2Name" val="Terran"/>
    <Constant name="Tab3Name" val="Zerg"/>
    <Constant name="Tab4Name" val="Protoss"/>
    <Constant name="Tab5Name" val="Feats of Strength"/>

    <!-- Stat Panels display Names -->
    <Constant name="Panel1HeaderTitle" val="Career"/>
    <Constant name="Category1HeaderTitle" val="Terran Career"/>
    <Constant name="Category2HeaderTitle" val="Zerg Career"/>
    <Constant name="Category3HeaderTitle" val="Protoss Career"/>
    <Constant name="Category4HeaderTitle" val="Neutral Career"/>
    <Constant name="Category1Button" val="Terran"/>
    <Constant name="Category2Button" val="Zerg"/>
    <Constant name="Category3Button" val="Protoss"/>
    <Constant name="Category4Button" val="Neutral"/>
    <!-- Standard Stats -->
    <Constant name="GlobalStat1Title" val="Games Played"/>
    <Constant name="GlobalStat2Title" val="Games Won"/>
    <Constant name="GlobalStat3Title" val="Rounds Survived"/>
    <Constant name="GlobalStat4Title" val="Rounds Cleared"/>
    <Constant name="GlobalStatHeader1" val="Hero Kills"/>
    <!-- Frame 1 Stats -->
    <Constant name="Category1Title1" val="Terran Hero 1 Kills"/>
    <Constant name="Category1Title2" val="Terran Hero 2 Kills"/>
    <Constant name="Category1Title3" val="Terran Hero 3 Kills"/>
    <!-- Frame 2 Stats -->
    <Constant name="Category2Title1" val="Zerg Hero 1 Kills"/>
    <Constant name="Category2Title2" val="Zerg Hero 2 Kills"/>
    <Constant name="Category2Title3" val="Zerg Hero 3 Kills"/>
    <!-- Frame 3 Stats -->
    <Constant name="Category3Title1" val="Protoss Hero 1 Kills"/>
    <Constant name="Category3Title2" val="Protoss Hero 2 Kills"/>
    <Constant name="Category3Title3" val="Protoss Hero 3 Kills"/>
    <!-- Frame 4 Stats -->
    <Constant name="Category4Title1" val="Global Stat 1"/>
    <Constant name="Category4Title2" val="Global Stat 2"/>
    <Constant name="Category4Title3" val="Global Stat 3"/>

    <!-- Last Match display Names -->

    <Constant name="Panel2HeaderTitle" val="Last Match"/>
    <Constant name="Panel2Title" val="Last Played"/>
```

## Updating to a Newer Version

If you're updating to a newer version of the libraries it isn't required to delete everything and start over, instead modular files are used that can be easily transfered over to the newer version, these files are contained in the following folders:

SCD-Achievements.SC2Mod\Base.SC2Data\GameData\UserData.xml - Contains achievements, in the case that achievements were added here instead of the Map itself

SCD-Achievements.SC2Mod\Base.SC2Data\UI\Layout\KL_DevPanels.SC2Layout - Contains Customized UI panels

SCD-Achievements.SC2Mod\Base.SC2Data\UI\Layout\KL_LocalizedText.SC2Layout - Contains Cusomizable Text

Backup these files before using the new mod version.

Once the files are saved, the older version must be deleted, replaced with the new version and your backed up files transfered to their locations.

Lastly, the Variable constant must be modified to the name of your bank.
