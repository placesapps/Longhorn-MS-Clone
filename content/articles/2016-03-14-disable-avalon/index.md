---
title: 'Hacking Avalon – 1: Disable it'
author: Melcher
type: post
date: 2016-03-14T22:01:47+00:00
url: /disable-avalon
featured_image: hackingavalon.png
categories:
  - Hacking Avalon

---
This is the first post in a series that I'll be doing. Hacking Avalon will be all about interesting stuff in Avalon. Furthermore, I hope to provide some background on how early variants of Avalon work together with the shell in Longhorn. Keep in mind, this series will mainly discuss the earliest revisions of Avalon found in the 3xxx range of builds. The tricks may not always work on later builds. That's it for the intro. Now onto the subject of this post; disabling Avalon in explorer.

The addition of Avalon to explorer makes for some interesting new functionality, but doesn’t exactly speed up browsing. There are a couple of ways to gracefully disable Avalon in explorer without breaking other Avalon features.

The first approach removes the task pane from explorer altogether. You will end up with just the listview. To achieve this, open System Properties (sysdm.cpl). Open the Advanced tab and Setting in the Performance settings. On the Visual Effects tab deselect ‘Use common tasks in folders’ and Apply.

The second approach will restore the classic task pane as seen in Windows XP. One registry key needs to be changed for this. In regedit browse to `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\WebView`.

Next, remove the GUID from the (Default) entry. This GUID tells explorer where to look for the Shell View provider which would normally be initialized via COM. Without this information explorer falls back to the older view. Note that while Avalon is disabled explorer will still happily display WinFS pivots in the task pane.

{{< figure src="explorer_w_avalon.png" title="With Avalon" >}}

{{< figure src="explorer_wo_avalon.png" title="Without Avalon" >}}