---
title: "4074.idx02"
type: build
url: /builds/4074
build_tag: "6.0.4074.0.idx02.040425-1535"
build_arch: [ "x86", "amd64", "ia64" ]
build_m: 7
install_date: "2004-04-26"
install_key: "TCP8W-T8PQJ-WWRRH-QH76C-99FBW"
featured_image: window-overview.png
---

This is the best known Longhorn build, it is generally known as the 'WinHEC 2004' build as it was given out there. It is from the Milestone 7 stage, still features the Slate theme, but with an updated wallpaper known as <i>Leaves.</i> It also contains a new theme called Jade and retains Windows XP's Luna as well as Windows Classic. This build also had a few cosmetic changes, like new icons in the Start Menu and Explorer. Windows Media Player has not been updated, however, Windows Messenger did get upgraded to 6.1 which changes the look. Creating new folders has been 'disabled' in this build. Applying the registry key below will enable folder creation.

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.Folder]
@="Folder"
```

A modified ISO has been released by Savoury and PandaX on BetaArchive in November 2011. This repack is known as TWIWMTB, short for _The Way It Was Meant To Be_. This repack includes a fully working Aurora Preview Panel Animation (APPA) and some minor fixes. TWIWMTB also has a DWM theme with transparency pre-installed. You can add APPA and Aero Glass to your vanilla Longhorn 4074 installation by [following this tutorial](/aurora-aero).

#### 64-bit
A 64-bit compile of this build is also available. As with the 4051 one, it still uses the i386 installation method but the basic VGA Driver has been updated so it works better after installation. As with the previous version, desktop applications and some Explorer dialogs are not included as well as the Sidebar.

### Gallery

{{< gallery 50 "window-overview.png" "aero-flip.png" >}}