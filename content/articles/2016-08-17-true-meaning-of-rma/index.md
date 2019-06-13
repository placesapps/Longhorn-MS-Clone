---
title: True meaning of RMA
author: Melcher
type: post
date: 2016-08-17T09:15:54+00:00
url: /true-meaning-of-rma
featured_image: /images/4008-rma-tile.png
categories:
  - Research

---

The _RMA test tile_ already caused some [discussion](http://www.betaarchive.com/forum/viewtopic.php?f=6&t=11052) in the past and nobody has since figured out what it’s purpose is. This hidden tile for the sidebar in builds 4008 and up has no obvious functionality other than taking up space. In this article we will dive into the real meaning and function of the RMA test tile.

![](/images/rma-tile.png)

If you were still wondering how to enable this tile in the first place, it's quite simple.

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\StartBar\Modules\RMA Test Tile]

"AssemblyName"="Microsoft.Windows.Client"
"Friendly Name"="RMA Test"
"Type"="System.Windows.Desktop.RMATestTile"
"Transient"=dword:00000000
```

There is not much we can make up out of the appearance of this tile. It displays a stretched copy of the Longhorn analog clock. Maybe the name can lead us somewhere: RMA. What does that mean? Surely, everybody who does online shopping knows what that means: _Return Merchandise Authorization_. This doesn’t really suit the context, however.

Turns out RMA is the abbreviation for a new kind of application introduced in Longhorn. I could no better explain it than [this snippet from the patent](https://patents.google.com/patent/US7669140B2 "Google Patents - System and method for providing rich minimized applications"):

> (&#8230;) Other tiles, known as transient tiles may include applications that exist outside the sidebar and are only present in the sidebar upon user request. For instance, a user can request that an application appear in the sidebar when it is minimized. The minimized application in the sidebar can provide basic functionality of the application without consuming excessive space. An application with this capability is referenced herein as a "rich minimized application" or "RMA".

![](/images/rma-registry.png)

As can be seen, the RMA Test Tile by default has its `Transient` property set to true. Only minimizing the associated application will make it visible. Unfortunately, no such application is supplied in any build. Setting `Transient` to false, will make this tile behave like a normal sidebar tile. Note that this tile doesn’t have any further specific behaviour or use: it just draws a placeholder image of the clock. _Nothing more, nothing less._

A _fine_ example of RMA is the use of a media player - which is actually implemented in several builds like the concept scenario below illustrates. Sadly, the images supplied with the patent filing are all black and white (which is a common thing for images that go with patents) and the image quality isn't all that great.

![](/images/US20050044058A1-20050224-D00014.png)

Here the media player is opened like usual and provides the full suite of functionality. The accompanying media player tile is transient and therefore hidden.

![](/images/US20050044058A1-20050224-D00015.png)

Upon minimizing the media player, the media player tile appears in the sidebar and offers basic functionality.

{{< figure src="/images/wmp-tile-concept.png" title="Media player tile close-up" >}}

## RMA today

With the sidebar being severely nerfed after the reset, RMA could never have been implemented as envisaged. The concept of rich minimized applications does, however, live on to this very day - Be it in another form. Instead of using the sidebar, applications may now provide functionality on the taskbar. As we saw in XP and Vista, Window Media Player provides basic play-back buttons once minimized in the form of a toolbar.

![](/images/rma-vista.jpg)

Functionality like this was  made available for developers as part of the platform with the introduction of Windows 7 in the form of [Thumbnail Toolbars](https://msdn.microsoft.com/en-us/library/windows/desktop/dd378460%28v=vs.85%29.aspx#thumbbars "MSDN - Taskbar Extensions").

![](/images/rma-win7.png)

> To provide access to a particular window's key commands without making the user restore or activate the application's window, an active toolbar control can be embedded in that window's thumbnail preview.

## Sidenote
The watchful reader may have noticed the glum looking frog in the background of the concept - wow your b/w recognition skills excellent. It looks like this concept is a design iteration in the ‘frog series’ like the one that can be seen in [this video](https://www.youtube.com/watch?v=HFTqOzKaSl8) by UXEvangelist.

![](/images/frog-concept-e2e-music.png)