# Luminosity theme for Windows 11 Taskbar Styler

**Author**: [mendes.image](https://github.com/mendesimage)

![Demonstration](dock.png)

## Intro
**Luminosity** is based on native Acrylic, using the maximum **TintLuminosityOpacity** value as its backdrop.

It's meant to be used with **Mica** or **MicaAlt** backdrops, with or without the **Translucent Windows** mod.

---

## Options

### Dock

![Dock](dock.png)

- Docks are cool.

### Classic

![Classic](classic.png)

- Meant to cause minimal disruption for users who prefer the classic Taskbar placement.

### Compact

![Compact](compact.png)

- Meant to be used with **Taskbar Labels for Windows 11**, using the **Centered Running Indicator** style, and **Taskbar Clock Customization**. Otherwise, you will experience visual issues.

### Mods Guide

To apply the same settings as mine, follow these steps:

* Open the **Taskbar Labels for Windows 11** and **Taskbar Clock Customization** mods in Windhawk.
* Go to the "Settings" tab and select "Textual mode".
* Copy the content below to the text box and click "Save settings".

**Taskbar Labels for Windows 11**
<details>
<summary>Click to expand mod settings</summary>

```yaml
mode: labelsWithoutCombining
taskbarItemWidth: 0
runningIndicatorStyle: centerDynamic
progressIndicatorStyle: centerDynamic
excludedPrograms:
  - excluded1.exe
minimumTaskbarItemWidth: 50
maximumTaskbarItemWidth: 176
fontSize: 12
fontFamily: ''
textTrimming: characterEllipsis
leftAndRightPaddingSize: 8
spaceBetweenIconAndLabel: 8
runningIndicatorHeight: 0
runningIndicatorVerticalOffset: 0
alwaysShowThumbnailLabels: 0
labelForSingleItem: '%name%'
labelForMultipleItems: '[%amount%] %name%'
```
</details>

**Taskbar Clock Customization**
<details>
<summary>Click to expand mod settings</summary>

```yaml
ShowSeconds: 1
TimeFormat: ''
DateFormat: ''
WeekdayFormat: dddd
WeekdayFormatCustom: Sun, Mon, Tue, Wed, Thu, Fri, Sat
TopLine: '%date%   %time%'
BottomLine: ''
MiddleLine: '%weekday%'
TooltipLine: ''
TooltipLineMode: append
Width: 180
Height: 60
MaxWidth: 0
TextSpacing: 0
DataCollection:
  NetworkMetricsFormat: mbs
  NetworkMetricsFixedDecimals: -1
  PercentageFormat: spacePaddingAndSymbol
  UpdateInterval: 1
  NetworkAdapterName: ''
  GpuAdapterName: ''
MediaPlayer:
  IgnoredPlayers:
    - ''
  MaxLength: 28
  NoMediaText: No media
  RemoveBrackets: 0
WebContentWeatherLocation: ''
WebContentWeatherFormat: '%c 🌡️%t 🌬️%w'
WebContentWeatherUnits: autoDetect
WebContentsItems:
  - Url: https://rss.nytimes.com/services/xml/rss/nyt/World.xml
    BlockStart: <item>
    Start: <title>
    End: </title>
    ContentMode: xmlHtml
    SearchReplace:
      - Search: ''
        Replace: ''
    MaxLength: 28
WebContentsUpdateInterval: 10
TimeZones:
  - Eastern Standard Time
TimeStyle:
  Hidden: 0
  TextColor: ''
  TextAlignment: ''
  FontSize: 0
  FontFamily: ''
  FontWeight: ''
  FontStyle: ''
  FontStretch: ''
  CharacterSpacing: 0
DateStyle:
  Hidden: 1
  TextColor: ''
  TextAlignment: ''
  FontSize: 0
  FontFamily: ''
  FontWeight: ''
  FontStyle: ''
  FontStretch: ''
  CharacterSpacing: 0
oldTaskbarOnWin11: 0
DataCollectionUpdateInterval: 1
```
</details>

---

## General Information

The theme changes the following elements:

- Taskbar Frame
- Taskbar Widget (compact version) \
  ![Widget](widget.png)
- Icon borders
- Taskbar icon sizes (compact version)
- Search icon with label
- Search box
- System Tray
    - Icon sizes (compact version)
    - Chevron icon border
    - Software icon border
    - Microphone icon border
    - Spacing between element groups
    - Tray Overflow Flyout
- Alt+Tab \
  ![Alt+Tab](alttab.png)
- Win+Tab background and Virtual Desktops bar
- Snap Bar and Picker
- Volume bar
- Window Preview Flyout \
  ![Window Preview Flyout](wpf.png)
- Context menus (with animations) \
  ![Menus](menu.png)
- Tooltips
- Removed drop shadows

## Guides

### Custom Animations Settings

To customize the animations, look for this style constant 
```
AnimationSettings=IsStaggeringEnabled="True" FromHorizontalOffset="-50" FromVerticalOffset="50"
```

- For all items to display immediately, set `IsStaggeringEnabled=` from `"True"` to `"False"`.

- `FromHorizontalOffset` and `FromVerticalOffset` are the directions where the items come from.
  - Horizontal **Positive** values is **Right**, **Negative** is **Left**.
  - Vertical **Positive** values is **Down**, **Negative** is **Up**.
  
### Custom Dock Width

The dock's width changes depending on your **screen resolution** using **horizontal margins**. If you want a custom width, follow this guide.

<details>
<summary>Click to expand guide</summary>

Locate and edit these `styleConstants` values:

  - DockMargin
  - DockMarginFix
  - DockTrayGap

The examples are for a **full length dock** (corner to corner).

## 1. Main taskbar width

`DockMargin=250`

This controls the main dock width.

- Smaller value = wider dock
- Larger value = narrower dock

Example: `DockMargin=5`

---

## 2. Background alignment fix

`DockMarginFix=500`

This value must always equal: `DockMargin × 2`

Example:

If: `DockMargin=5`

Then: `DockMarginFix=10`

---

## 3. System Tray margin for extra space

`DockTrayGap=-307`

This controls the spacing between the taskbar icons and the system tray.

Formula: `-(DockMargin + 57)`

Example:

If: `DockMargin=5`

Then: `DockTrayGap=-62`

---

**⚠️ Important notes**

- Forgetting the **minus sign** (`-`) will break the alignment.
- If the **Right** values do not match, the tray alignment will be incorrect.
- The **Left** value reduces the gap between the taskbar icons and the system tray.
- Large changes may require small adjustments depending on your custom setting, especially when the taskbar is almost full.
</details>

---

## Known Issues

I didn't know how to fix these. I couldn't find the correct target names, or I'm not sure if they can even be changed/fixed.

- **Widget/Weather:** The bottom text line has incorrect placement in **Compact version** (renders off-screen).
- **Icon Hitboxes (Dock):** The Taskbar's rounded corners slightly limit the icon hitbox on the **top and bottom**, which makes it **impossible to minimize windows by clicking in those areas**.
- **Left Taskbar Alignment (Dock):** When using **Left Taskbar Alignment**, the Widget clip into the **SystemTray**. As a workaround: In `styleConstants`, change: `DockTrayGap=-307`  to `DockTrayGap=-261`

- **SearchBox (Dock/Classic):** Has **mismatched look and position** when typing.
- **SearchBox (Compact):** Has incorrect styling and positioning in the Compact version.
- **`Taskbar height and icon size` incompatibility (Dock/Compact):** to make it compatible, locate the target `Taskbar.TaskbarFrame` and delete the line `- Height=58`

---

## Theme selection

The theme is integrated into the mod and can be selected directly from the mod's
settings:

* Open the Windows 11 Taskbar Styler mod in Windhawk.
* Go to the "Settings" tab.
* Select the theme and save the settings.

## Manual installation

The theme styles can also be imported manually. To do that, follow these steps:

* Open the Windows 11 Taskbar Styler mod in Windhawk.
* Go to the "Settings" tab and select "Textual mode".
* Copy the content below to the text box and click "Save settings".

---

### Dock

<details>
<summary>Content to import (click to expand)</summary>

```yaml
styleConstants:
  - DockMargin=250
  - DockMarginFix=500
  - DockTrayGap=-307
  - AnimationSettings=IsStaggeringEnabled="True" FromHorizontalOffset="-50" FromVerticalOffset="50"
  - mbg=<WindhawkBlur BlurAmount="30" TintColor="{ThemeResource CardStrokeColorDefaultSolid}" TintOpacity="0.0" TintLuminosityOpacity="1.0" TintSaturation="1.0" NoiseDensity="1.0" NoiseOpacity="0.1" />
  - bcr=10
  - wcr=20
  - mcr=15
  - t=Transparent
  - bb=#20FFFFFF
  - bt=1
  - bt2=2
  - nbb=<LinearGradientBrush x:Key="ShellTaskbarItemGradientStrokeColorSecondaryBrush" MappingMode="Absolute" StartPoint="0,0" EndPoint="0,3"><LinearGradientBrush.GradientStops><GradientStop Offset="0.33" Color="#1AFFFFFF" /><GradientStop Offset="1" Color="#0FFFFFFF" /></LinearGradientBrush.GradientStops></LinearGradientBrush>
  - nbt=<SolidColorBrush Color="{ThemeResource ControlFillColorDefault}" />
  - nbth=<SolidColorBrush Color="{ThemeResource ControlFillColorSecondary}" />
  - nbtp=<SolidColorBrush Color="{ThemeResource ControlFillColorTertiary}" />
controlStyles:
  - target: Taskbar.TaskbarFrame > Grid#RootGrid > Taskbar.TaskbarBackground > Grid > Rectangle#BackgroundFill
    styles:
      - Fill:=$mbg
  - target: Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Taskbar.ExperienceToggleButton
    styles:
      - CornerRadius=$bcr
  - target: Taskbar.TaskListButton
    styles:
      - CornerRadius=$bcr
  - target: SearchUx.SearchUI.SearchButtonRootGrid#SearchBoxButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#SearchPillBackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#MultiWindowElement
    styles:
      - CornerRadius=$bcr
  - target: SystemTray.ChevronIconView > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=0,4,2,4
  - target: SystemTray.NotifyIconView > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.IconView#SystemTrayIcon > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.OmniButton#ControlCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.OmniButton#NotificationCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: Border#OverflowFlyoutBackgroundBorder
    styles:
      - Background:=$mbg
      - CornerRadius:=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Taskbar.OverflowToggleButton#OverflowButton > Taskbar.TaskListButtonPanel#OverflowToggleButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Grid#ConfirmatorMainGrid
    styles:
      - Background:=$mbg
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Shapes.Rectangle#HorizontalTrackRect
    styles:
      - Fill:=#10FFFFFF
  - target: Taskbar.TaskbarBackground#HoverFlyoutBackgroundControl > Grid > Rectangle#BackgroundFill
    styles:
      - Fill:=$t
  - target: Windows.UI.Xaml.Controls.Grid#HoverFlyoutGrid > Windows.UI.Xaml.Controls.Border#HoverFlyoutBackground
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Taskbar.TaskItemThumbnailView > Grid@CommonStates > Border#BackgroundBorder
    styles:
      - Background=$t
      - CornerRadius=$mcr
      - BorderThickness@Normal=0
      - BorderBrush@Normal=$t
      - BorderThickness@PointerOver=0.05,0,0.05,2
      - BorderBrush@PointerOver:=<SolidColorBrush Color="{ThemeResource SystemAccentColorLight2}" Opacity="1.0" />
  - target: Windows.UI.Xaml.Controls.Button#CloseButton
    styles:
      - CornerRadius=$mcr
  - target: Taskbar.ThumbBarButton#ThumbBarButton > Windows.UI.Xaml.Controls.ContentPresenter#BorderElement@CommonStates
    styles:
      - CornerRadius=16
      - Margin=-1.5,-1.5,-1.5,-1.5
      - Background@Disabled:=$t
      - Background@Normal:=$t
      - Background@PointerOver:=$nbth
      - Background@Pressed:=$nbtp
      - BorderThickness=$bt2
      - BorderBrush@Disabled:=$t
      - BorderBrush@Normal:=$t
      - BorderBrush@PointerOver:=$nbb
      - BorderBrush@Pressed:=$nbb
      - BackgroundSizing=InnerBorderEdge
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.200" />
  - target: Windows.UI.Xaml.Controls.Grid#ModalRootGrid > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - Background=Transparent
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#ModalRootGrid > Windows.UI.Xaml.Controls.Border#BackgroundElement > WindowsInternal.ComposableShell.Experiences.Switcher.SwitchItemList
    styles:
      - Background:=$mbg
  - target: Windows.UI.Xaml.Controls.Border#BackgroundDimmingLayer
    styles:
      - Background:=<WindhawkBlur BlurAmount="0" TintColor="#00000000" />
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement#VirtualDesktopBar > Grid > Border
    styles:
      - Background:=$mbg
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Margin=0,2,0,-1
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement#VirtualDesktopBar
    styles:
      - Width=Auto
      - HorizontalAlignment=1
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement > Windows.UI.Xaml.Controls.Grid#GridElement > Windows.UI.Xaml.Controls.Border#VirtualDesktopSwitcherBackground
    styles:
      - BorderThickness=$bt
      - BorderBrush=$bb
      - CornerRadius=$mcr
      - Margin=0,2,0,2
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement > Grid > Border
    styles:
      - Background:=$mbg
      - Shadow:=
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopElementThemed > Windows.UI.Xaml.Controls.Grid#MainGrid@CommonStates
    styles:
      - CornerRadius=$mcr
      - Background@PointerOverListItem:=$nbth
      - Background@PointerNotOverListItem:=$t
      - Background@NotActiveDesktop:=$t
      - Background@NotActiveDesktopPointerOver:=$t
      - Background@NotActiveDesktopPointerOver2:=$t
      - Background@NotActiveDesktopDragOver:=$t
      - Background@ActivityStateFocused:=$nbt
      - Background@ActiveDesktop:=$nbt
      - Background@ActiveDesktopPointerOver:=$nbth
      - Background@ActiveDesktopPointerOver2:=$nbth
      - Background@ActiveDesktopDragOver:=$nbtp
      - Background@RenameVirtualDesktop:=$nbth
      - Background@RenameVirtualDesktopFinished:=$nbth
      - BorderThickness=$bt2
      - BorderBrush@PointerOverListItem:=$nbb
      - BorderBrush@PointerNotOverListItem:=$t
      - BorderBrush@NotActiveDesktop:=$t
      - BorderBrush@NotActiveDesktopPointerOver:=$t
      - BorderBrush@NotActiveDesktopPointerOver2:=$t
      - BorderBrush@NotActiveDesktopDragOver:=$t
      - BorderBrush@NotActiveDesktop:=$t
      - BorderBrush@ActivityStateFocused:=$nbb
      - BorderBrush@ActiveDesktop:=$nbb
      - BorderBrush@ActiveDesktopPointerOver:=$nbb
      - BorderBrush@ActiveDesktopPointerOver2:=$nbb
      - BorderBrush@ActiveDesktopDragOver:=$nbb
      - BorderBrush@RenameVirtualDesktop:=$nbb
      - BorderBrush@RenameVirtualDesktopFinished:=$nbb
      - BackgroundSizing=InnerBorderEdge
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopElementThemed > Windows.UI.Xaml.Controls.Grid#MainGrid > Windows.UI.Xaml.Controls.Border#MainBorder
    styles:
      - CornerRadius=$mcr
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopElementThemed > Windows.UI.Xaml.Controls.Grid#MainGrid > Windows.UI.Xaml.Controls.Border#BorderHighlight
    styles:
      - CornerRadius=$mcr
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopElementThemed > Windows.UI.Xaml.Controls.Grid#MainGrid > Windows.UI.Xaml.Controls.Border#ActiveDesktopPill
    styles:
      - CornerRadius=$mcr
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.NewVirtualDesktopElementThemed#NewVirtualDesktopButtonThemed > Windows.UI.Xaml.Controls.Grid#MainGrid@CommonStates
    styles:
      - CornerRadius=$mcr
      - Margin=2,2,2,2
      - Background@DragOver:=$t
      - Background@NotDragOver :=$t
      - Background@NotActiveDesktopPointerOver:=$nbth
      - BorderThickness=$bt2
      - BorderBrush@DragOver:=$t
      - BorderBrush@NotDragOver :=$t
      - BorderBrush@NotActiveDesktopPointerOver:=$nbb
      - BackgroundSizing=InnerBorderEdge
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.NewVirtualDesktopElementThemed#NewVirtualDesktopButtonThemed > Windows.UI.Xaml.Controls.Grid#MainGrid > Windows.UI.Xaml.Controls.Border#MainBorder
    styles:
      - CornerRadius=$mcr
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.NewVirtualDesktopElementThemed#NewVirtualDesktopButtonThemed > Windows.UI.Xaml.Controls.Grid#MainGrid > Windows.UI.Xaml.Controls.Border#BorderHighlight
    styles:
      - CornerRadius=$mcr
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.NewVirtualDesktopElementThemed#NewVirtualDesktopButtonThemed > Windows.UI.Xaml.Controls.Grid#MainGrid > Windows.UI.Xaml.Controls.Border#ActiveDesktopPill
    styles:
      - CornerRadius=$mcr
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.SwitchItemListViewItem > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.SwitchItemThumbnailButton#ThumbnailHost > Windows.UI.Xaml.Controls.Grid#RootGrid
    styles:
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.Button#VirtualDesktopElementCloseButton
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#SnapBarBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - RenderTransform:=<TranslateTransform X="0" Y="-20" />
      - Margin=0,0,0,-10
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Border#SnapPickerBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.FlyoutPresenter > Border
    styles:
      - Shadow:=
  - target: MenuFlyoutPresenter
    styles:
      - CornerRadius=$mcr
      - Shadow:=
  - target: MenuFlyoutPresenter > Border
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.MenuFlyoutItem
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.MenuFlyoutSubItem
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.ToolTip > Windows.UI.Xaml.Controls.ContentPresenter#LayoutRoot
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: ScrollViewer#MenuFlyoutPresenterScrollViewer > Border > Grid > ScrollContentPresenter > ItemsPresenter > StackPanel
    styles:
      - ChildrenTransitions:=<TransitionCollection><EntranceThemeTransition $AnimationSettings /></TransitionCollection>
  - target: Grid#LayoutRoot
    styles:
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: Border#BackgroundBorder
    styles:
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: Taskbar.TaskbarFrame > Grid#RootGrid > Taskbar.TaskbarBackground > Grid > Rectangle#BackgroundFill
    styles:
      - Visibility=Collapsed
  - target: Taskbar.TaskbarFrame
    styles:
      - Height=58
      - Margin=$DockMargin,0,$DockMargin,0
  - target: Taskbar.TaskbarFrame > Grid#RootGrid
    styles:
      - Background:=$mbg
      - BorderThickness=$bt
      - BorderBrush:=$bb
      - CornerRadius=$mcr
      - Margin=0,5,$DockMarginFix,5
  - target: Taskbar.TaskbarBackground#BackgroundControl > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Shapes.Rectangle#BackgroundStroke
    styles:
      - Visibility=Collapsed
  - target: Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel > Windows.UI.Xaml.Controls.Grid#AugmentedEntryPointContentGrid
    styles:
      - RenderTransform:=<TranslateTransform X="0" Y="-1" />
  - target: Taskbar.AugmentedEntryPointButton#AugmentedEntryPointButton
    styles:
      - Margin=0,0,-57,0
  - target: Windows.UI.Xaml.Controls.Border#LargeTicker1
    styles:
      - Margin=0,0,0,-4
  - target: Grid#SystemTrayFrameGrid
    styles:
      - Margin=$DockTrayGap,0,$DockMargin,0
      - HorizontalAlignment=Right
```
</details>

---

### Classic

<details>
<summary>Content to import (click to expand)</summary>

```yaml
styleConstants:
  - mbg=<WindhawkBlur BlurAmount="30" TintColor="{ThemeResource CardStrokeColorDefaultSolid}" TintOpacity="0.0" TintLuminosityOpacity="1.0" TintSaturation="1.0" NoiseDensity="1.0" NoiseOpacity="0.1" />
  - bcr=10
  - wcr=20
  - mcr=15
  - t=Transparent
  - bb=#20FFFFFF
  - bt=1
  - AnimationSettings=<TransitionCollection><EntranceThemeTransition IsStaggeringEnabled="True" FromHorizontalOffset="-50" FromVerticalOffset="50" /></TransitionCollection>
controlStyles:
  - target: Taskbar.TaskbarFrame > Grid#RootGrid > Taskbar.TaskbarBackground > Grid > Rectangle#BackgroundFill
    styles:
      - Fill:=$mbg
  - target: Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Taskbar.ExperienceToggleButton
    styles:
      - CornerRadius=$bcr
  - target: Taskbar.TaskListButton
    styles:
      - CornerRadius=$bcr
  - target: SearchUx.SearchUI.SearchButtonRootGrid#SearchBoxButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#SearchPillBackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#MultiWindowElement
    styles:
      - CornerRadius=$bcr
  - target: SystemTray.ChevronIconView
    styles:
      - CornerRadius=$bcr
      - Margin=0,0,2,0
  - target: SystemTray.NotifyIconView > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.IconView#SystemTrayIcon > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.OmniButton#ControlCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.OmniButton#NotificationCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: Border#OverflowFlyoutBackgroundBorder
    styles:
      - Background:=$mbg
      - CornerRadius:=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#ConfirmatorMainGrid
    styles:
      - Background:=$mbg
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Shapes.Rectangle#HorizontalTrackRect
    styles:
      - Fill:=#10FFFFFF
  - target: Taskbar.TaskbarBackground#HoverFlyoutBackgroundControl > Grid > Rectangle#BackgroundFill
    styles:
      - Fill:=$t
  - target: Windows.UI.Xaml.Controls.Grid#HoverFlyoutGrid > Windows.UI.Xaml.Controls.Border#HoverFlyoutBackground
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Taskbar.TaskItemThumbnailView > Grid@CommonStates > Border#BackgroundBorder
    styles:
      - Background=$t
      - CornerRadius=$mcr
      - BorderThickness@Normal=0
      - BorderBrush@Normal=$t
      - BorderThickness@PointerOver=0.05,0,0.05,2
      - BorderBrush@PointerOver:=<SolidColorBrush Color="{ThemeResource SystemAccentColorLight2}" Opacity="1.0" />
  - target: Windows.UI.Xaml.Controls.Button#CloseButton
    styles:
      - CornerRadius=$mcr
  - target: Windows.UI.Xaml.Controls.ContentPresenter#BorderElement
    styles:
      - CornerRadius=16
      - Margin=-1,-1,-1,-1
  - target: Windows.UI.Xaml.Controls.Grid#ModalRootGrid > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - Background=Transparent
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#ModalRootGrid > Windows.UI.Xaml.Controls.Border#BackgroundElement > WindowsInternal.ComposableShell.Experiences.Switcher.SwitchItemList
    styles:
      - Background:=$mbg
  - target: Windows.UI.Xaml.Controls.Border#BackgroundDimmingLayer
    styles:
      - Background:=<WindhawkBlur BlurAmount="0" TintColor="#00000000" />
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement#VirtualDesktopBar > Grid > Border
    styles:
      - Background:=$mbg
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement#VirtualDesktopBar
    styles:
      - MaxWidth:=900
      - Shadow:=
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement > Windows.UI.Xaml.Controls.Grid#GridElement > Windows.UI.Xaml.Controls.Border#VirtualDesktopSwitcherBackground
    styles:
      - BorderThickness=$bt
      - BorderBrush=$bb
      - CornerRadius=$mcr
      - Margin=0,0,1,0
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement > Grid > Border
    styles:
      - Background:=$mbg
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#MainGrid
    styles:
      - CornerRadius=13
  - target: Windows.UI.Xaml.Controls.Button#VirtualDesktopElementCloseButton
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#SnapBarBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - RenderTransform:=<TranslateTransform X="0" Y="-20" />
      - Margin=0,0,0,-10
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Border#SnapPickerBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.FlyoutPresenter > Border
    styles:
      - Shadow:=
  - target: MenuFlyoutPresenter
    styles:
      - CornerRadius=$mcr
      - Shadow:=
  - target: MenuFlyoutPresenter > Border
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.MenuFlyoutItem
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.MenuFlyoutSubItem
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.ToolTip > Windows.UI.Xaml.Controls.ContentPresenter#LayoutRoot
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: ScrollViewer#MenuFlyoutPresenterScrollViewer > Border > Grid > ScrollContentPresenter > ItemsPresenter > StackPanel
    styles:
      - ChildrenTransitions:=$AnimationSettings
  - target: Grid#LayoutRoot
    styles:
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: Border#BackgroundBorder
    styles:
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: Microsoft.UI.Xaml.Controls.ItemsRepeater#TaskbarFrameRepeater
    styles:
      - Margin=0,1,0,0
  - target: SystemTray.ChevronIconView
    styles:
      - Margin=0,1,2,0
  - target: SystemTray.NotifyIconView > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - Margin=2,5,2,4
  - target: SystemTray.IconView#SystemTrayIcon > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - Margin=2,5,2,4
  - target: SystemTray.OmniButton#ControlCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - Margin=2,5,2,4
  - target: SystemTray.OmniButton#NotificationCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - Margin=2,5,2,4
```
</details>

---

### Compact

<details>
<summary>Content to import (click to expand)</summary>

```yaml
styleConstants:
  - mbg=<WindhawkBlur BlurAmount="30" TintColor="{ThemeResource CardStrokeColorDefaultSolid}" TintOpacity="0.0" TintLuminosityOpacity="1.0" TintSaturation="1.0" NoiseDensity="1.0" NoiseOpacity="0.1" />
  - bcr=10
  - wcr=20
  - mcr=15
  - t=Transparent
  - bb=#20FFFFFF
  - bt=1
  - AnimationSettings=<TransitionCollection><EntranceThemeTransition IsStaggeringEnabled="True" FromHorizontalOffset="-50" FromVerticalOffset="50" /></TransitionCollection>
controlStyles:
  - target: Taskbar.TaskbarFrame > Grid#RootGrid > Taskbar.TaskbarBackground > Grid > Rectangle#BackgroundFill
    styles:
      - Fill:=$mbg
  - target: Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Taskbar.ExperienceToggleButton
    styles:
      - CornerRadius=$bcr
  - target: Taskbar.TaskListButton
    styles:
      - CornerRadius=$bcr
  - target: SearchUx.SearchUI.SearchButtonRootGrid#SearchBoxButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#SearchPillBackgroundElement
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#MultiWindowElement
    styles:
      - CornerRadius=$bcr
  - target: SystemTray.ChevronIconView
    styles:
      - CornerRadius=$bcr
      - Margin=0,0,2,0
  - target: SystemTray.NotifyIconView > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.IconView#SystemTrayIcon > Windows.UI.Xaml.Controls.Grid#ContainerGrid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.OmniButton#ControlCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: SystemTray.OmniButton#NotificationCenterButton > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.Border#BackgroundBorder
    styles:
      - CornerRadius=$bcr
      - Margin=2,4,2,4
  - target: Border#OverflowFlyoutBackgroundBorder
    styles:
      - Background:=$mbg
      - CornerRadius:=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#ConfirmatorMainGrid
    styles:
      - Background:=$mbg
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Shapes.Rectangle#HorizontalTrackRect
    styles:
      - Fill:=#10FFFFFF
  - target: Taskbar.TaskbarBackground#HoverFlyoutBackgroundControl > Grid > Rectangle#BackgroundFill
    styles:
      - Fill:=$t
  - target: Windows.UI.Xaml.Controls.Grid#HoverFlyoutGrid > Windows.UI.Xaml.Controls.Border#HoverFlyoutBackground
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Taskbar.TaskItemThumbnailView > Grid@CommonStates > Border#BackgroundBorder
    styles:
      - Background=$t
      - CornerRadius=$mcr
      - BorderThickness@Normal=0
      - BorderBrush@Normal=$t
      - BorderThickness@PointerOver=0.05,0,0.05,2
      - BorderBrush@PointerOver:=<SolidColorBrush Color="{ThemeResource SystemAccentColorLight2}" Opacity="1.0" />
  - target: Windows.UI.Xaml.Controls.Button#CloseButton
    styles:
      - CornerRadius=$mcr
  - target: Windows.UI.Xaml.Controls.ContentPresenter#BorderElement
    styles:
      - CornerRadius=16
      - Margin=-1,-1,-1,-1
  - target: Windows.UI.Xaml.Controls.Grid#ModalRootGrid > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - Background=Transparent
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#ModalRootGrid > Windows.UI.Xaml.Controls.Border#BackgroundElement > WindowsInternal.ComposableShell.Experiences.Switcher.SwitchItemList
    styles:
      - Background:=$mbg
  - target: Windows.UI.Xaml.Controls.Border#BackgroundDimmingLayer
    styles:
      - Background:=<WindhawkBlur BlurAmount="0" TintColor="#00000000" />
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement#VirtualDesktopBar > Grid > Border
    styles:
      - Background:=$mbg
      - CornerRadius=$wcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement#VirtualDesktopBar
    styles:
      - MaxWidth:=900
      - Shadow:=
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement > Windows.UI.Xaml.Controls.Grid#GridElement > Windows.UI.Xaml.Controls.Border#VirtualDesktopSwitcherBackground
    styles:
      - BorderThickness=$bt
      - BorderBrush=$bb
      - CornerRadius=$mcr
      - Margin=0,0,1,0
  - target: WindowsInternal.ComposableShell.Experiences.Switcher.VirtualDesktopBarElement > Grid > Border
    styles:
      - Background:=$mbg
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Grid#MainGrid
    styles:
      - CornerRadius=13
  - target: Windows.UI.Xaml.Controls.Button#VirtualDesktopElementCloseButton
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.Border#SnapBarBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - RenderTransform:=<TranslateTransform X="0" Y="-20" />
      - Margin=0,0,0,-10
      - Shadow:=
  - target: Windows.UI.Xaml.Controls.Border#SnapPickerBorder
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.FlyoutPresenter > Border
    styles:
      - Shadow:=
  - target: MenuFlyoutPresenter
    styles:
      - CornerRadius=$mcr
      - Shadow:=
  - target: MenuFlyoutPresenter > Border
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
  - target: Windows.UI.Xaml.Controls.MenuFlyoutItem
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.MenuFlyoutSubItem
    styles:
      - CornerRadius=$bcr
  - target: Windows.UI.Xaml.Controls.ToolTip > Windows.UI.Xaml.Controls.ContentPresenter#LayoutRoot
    styles:
      - Background:=$mbg
      - CornerRadius=$mcr
      - BorderThickness=$bt
      - BorderBrush=$bb
      - Shadow:=
  - target: ScrollViewer#MenuFlyoutPresenterScrollViewer > Border > Grid > ScrollContentPresenter > ItemsPresenter > StackPanel
    styles:
      - ChildrenTransitions:=$AnimationSettings
  - target: Grid#LayoutRoot
    styles:
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: Border#BackgroundBorder
    styles:
      - BackgroundTransition:=<BrushTransition Duration="0:0:0.100" />
  - target: Taskbar.TaskbarFrame
    styles:
      - Height=30
  - target: Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel > Windows.UI.Xaml.Controls.Grid#AugmentedEntryPointContentGrid
    styles:
      - RenderTransform:=<TranslateTransform X="0" Y="-1" />
  - target: Windows.UI.Xaml.Controls.Border#LargeTicker1
    styles:
      - Margin=1,-5,0,0
      - RenderTransform:=<ScaleTransform ScaleX="0.75" ScaleY="0.75" />
  - target: SearchUx.SearchUI.SearchButtonRootGrid#SearchBoxButtonRootPanel > Windows.UI.Xaml.Controls.Border#BackgroundElement
    styles:
      - Margin=0,4,0,4
  - target: SearchUx.SearchUI.SearchButtonControl
    styles:
      - Margin=0,-4,0,-4
  - target: Microsoft.UI.Xaml.Controls.AnimatedVisualPlayer#Icon
    styles:
      - Width=16
      - Height=16
  - target: Windows.UI.Xaml.Controls.Image#Icon
    styles:
      - Width=16
      - Height=16
  - target: Taskbar.TaskListButton#TaskListButton > Taskbar.TaskListLabeledButtonPanel#IconPanel > Windows.UI.Xaml.Controls.TextBlock#LabelControl
    styles:
      - RenderTransform:=<TranslateTransform X="0" Y="-1" />
  - target: Grid#SystemTrayFrameGrid
    styles:
      - Margin=0,0,0,18
  - target: SystemTray.TextIconContent > Grid#ContainerGrid > SystemTray.AdaptiveTextBlock#Base > TextBlock#InnerTextBlock
    styles:
      - FontSize=14
  - target: SystemTray.ImageIconContent > Grid#ContainerGrid > Image
    styles:
      - Width=14
      - Height=14
```
</details>
