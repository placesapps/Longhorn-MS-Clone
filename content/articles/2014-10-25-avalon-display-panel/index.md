---
title: Avalon Display Panel
author: Melcher
type: post
date: 2014-10-25T19:33:31+00:00
url: /avalon-display-panel/
featured_image: display-panel-3683.png
categories:
  - Features

---

There are two distinct "new" display control panels developed prior to the Longhorn reset. The first appeared in Milestone 3, and was removed in early Milestone 4. The second was present only in [build 4093](/builds/4093/). Though both are created in the Avalon UI framework, it seems almost certain that the two efforts were not connected beyond their functionality and underlying technology.

#### Milestone 3

In [build 3683](/builds/3683/), it is accessible out-of-the-box by right-clicking on the desktop and selecting Properties from the right click menu, as one would with any previous version of Windows. The Avalon display panel in 3683 has a number of bugs however. Later builds do not have this new panel enabled out of the box. Once enabled though, they have even further bugs, caused by a lack of further development to ensure that it remained compatible with the rapidly changing Avalon framework. The last confirmed build to contain the Milestone 3 Avalon display panel is [4001](/builds/4001/).

![](display-panel-3683.png)

It was first activated in one of the other Milestone 3 builds as part of the protoPlex Project in early 2008. It was achieved by simply copying in the 3683 desk.cpl, and executing that rather than the version native to that build. This step was then forgotten about and was not investigated further. In 2012, this screenshot was rediscovered, prompting further investigation. This investigation has revealed that it can be enabled in other Milestone 3 builds by simply using the registry file below:

{{< highlight reg >}}
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Control Panel\Desktop]
"ClassicDisplayCPL"=dword:00000000
{{< / highlight >}}

This value is checked in all builds with the display panel present. However, there is a difference between the check in 3683 and later builds which explains why it works out of the box in 3683, but requires the value set in later builds. In 3683, the display panel is shown if the `SHRegGetValueW` call fails or the returned value is not 1. In later builds, this has been fixed so that the display panel is only shown if the `SHRegGetValueW` call succeeds or the value returned is 1. Logically, the latter behaviour is correct, so it makes sense to reason that this was a bug fix by Microsoft. With the original check, the `SHRegGetValueW` call could fail for any number of reasons, and not just because the registry key is not present, potentially causing unintended side-effects.

![](display-panel-3718.png)

As you can see from the above screenshot, in later builds, there are some rendering errors. This confirms previous suspicions that development of this feature was insufficient to retain full compatibility with the rapid development of the Avalon framework at the time. This would also explain why the feature was cut at the start of Milestone 4.

#### Milestone 7

In build 4093, you have to run `lhdesk.exe` in order to access the display panel. There is no option to integrate it into the existing user interface. The display panel bares little resemblance to the earlier effort.

![](display-panel-4093.png)