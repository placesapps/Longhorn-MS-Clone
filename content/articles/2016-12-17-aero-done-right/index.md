---
title: Aero done right
author: Melcher
type: post
date: 2016-12-17T13:49:43+00:00
url: /aero-done-right/
featured_image: 4074-dwm-jade.png
categories:
  - Features
  - User Guides

---
A lot of people have been struggling to get Aero to work in build 4074. In this post I want to show you how Aero can be enabled along with a little bit of its history. If you came here looking for information about Aurora, please see my post about [Aurora & Aero](/aurora-aero/).

#### A theme with two faces

During the development of Longhorn the exact look of the Aero theme was kept a good secret. Aero remained off-limits even for most shell developers. Two developers that surely had access are [Kam Vedbrat](https://blogs.msdn.microsoft.com/kamvedbrat/2004/09/28/kams-new-job/ "Kam Vedbrat, MSDN Blogs - Kam's new job") and Scott Hanggie. Until September 2004, Kam Vedbrat had been a lead program manager on the Aero effort by the shell team. [On Channel9](https://channel9.msdn.com/Blogs/scobleizer/Kam-Vedbrat-Looking-at-Windows-Vistas-user-interface-AERO "Robert Scoble, Channel9 - Kam Vedbrat Looking at Windows Vistas user interface AERO"), he elaborates on how Aero is designed.

According to internal documentation, personal authorization by Scott Hanggie was required to get access to the Aero theme files. Scott is also one of the patent holders for the _Compositing Desktop Window Manager_. The screenshot below is part of that very patent filing. The image shows some of Aero's most notable features: aurora in the preview panel and transparent borders - features that were, at the time, still highly confidential.

{{< figure src="aero-pat.png" title="Note that only the border is transparent. Probably, MILExplorer has not been set in the registry." >}}

Although there is no way to tell when this screenshot was taken and on which build, I tend to think it was taken on one of the many 4050 [lab06_demo](/builds/branch/lab06/lab06_demo/) builds compiled during 2003 leading up to the [PDC 2003 demo build](/builds/4050-pdc/). By default the build from the lab06_demo branch had an appearance similar (if not identical) to the publicly released build at PDC 2003, [4051](/builds/4051/). In contrast to the public build these builds, however, did have full support for Aero. The sad news that the public build would not yet feature Aero was brought by [Paul Thurrott](http://web.archive.org/web/20060310222543/http://www.windowsitpro.com/Articles/Index.cfm?ArticleID=40367%26DisplayTab=Article "Windows IT Pro - Exclusive: PDC Attendees to Get Aero Demo Only") in September:

> For the past several weeks, Microsoft has forked the Longhorn code to develop a special PDC build that's separate and distinct from the main code fork. This build will include virtually every Longhorn technology except Aero(&#8230;)

Not only was Aero missing, but the complete DWM system was crippled. Even ordinary Microsoft employees couldn't get their hands on all the shiny Aero stuff. Instead, developers were to use the placeholder _Jade_ theme. This theme had a far less attractive silvery finish and borders weren't transparent, but instead an ugly greenish color. This short video snippet taken during PDC 2003 by Paul Thurrott and Keith Furman makes apparent that Aero just wasn't for everyone yet.

<video width="100%" preload="metadata" controls="controls">
  <source type="video/mp4" src="pdc2003_aero_3d_effects.mp4" />
  <a href="pdc2003_aero_3d_effects.mp4">Download video</a>
</video>

When build 4074 was given to attendees of the WinHEC 2004 event people immediately started wondering whether Aero was present in this build as well. In a webcast , highlighting the progress made in build 4074 technical evangelist [Dave Massy said](https://blogs.msdn.microsoft.com/tims/2004/05/08/longhorn-winhec-build-whats-new/ "Tim Sneath, MSDN Blogs - Longhorn WinHEC Build: What's New?"):

> You are not going to notice a huge visual difference from the previous builds of Longhorn. We still have a lot of work before we actually turn on the next-generation user experience.

Although Microsoft employees denied any claims of Aero and DWM being present and even claiming that it was left out this build on purpose, DWM was found working in build 4074. It was discovered that the Jade theme present in builds 4066 and up could unlock parts of the Aero style.


#### Getting ourselves some Aero

Before trying to enable Aero be sure to have a look at this post I wrote earlier: [Destkop Compositing](/desktop-compositing/). On that page I explain everything you need to know to get DWM working on your (virtual) machine. So, go have a look there - I'll wait.

Okay, done that? Now that you have installed the proper drivers, it’s probably a good thing to reboot the computer for the changes to take affect (if you haven't do so already).

To convert Jade to Aero you need to rename the theme files and edit the .theme file. If you are using the ‘TWIWMTB’ 4074 version you can skip the rest of this step and head on to the next one.

  * Browse to `C:\Windows\Resources\Themes\` and copy the file jade.theme and the jade folder to another directory
  * Rename jade.theme and jade.msstyles to respectively aero.theme and aero.msstyles. Rename the folder to aero too.
  * Open the aero.theme with notepad or wordpad and change `DisplayName=@themeui.dll,-203` to `DisplayName=Aero`
  * Next, replace the remaining two instances of the word `jade` in the same file with `aero` (use CTRL+H)
  * Copy the newly created aero.theme and the aero folder back in the `C:\Windows\Resources\Themes\` directory

#### Transparency

Now we are going to enable the beautiful transparency that we so longed for. Okay, wait a sec here. Since the original Jade theme doesn't have the transparent PNGs you will - in the case you're using the original files - not end up with truly transparent borders. You're better of using a patched Aero theme file or the TWIWMTB build which has a patched theme file pre-installed.

All we need to do is add a registry key. Open the registry editor (regedit). Browse to: `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer`. In this key ad a DWORD called MILExplorer and set its value to 1. If you would also like to enable the Aero stars, also add a DWORD called MILDesktop with the value of 1. The moment has come to get a glimpse of Longhorn glory: go to Display Properties and choose the newly created Aero theme. Apply the settings. After the theme is applied you will be greeted by a nice transparent taskbar and sidebar.

**At this point, it’s not possible to open any explorer windows as they will not show up on the screen. To fix this, proceed to the next step.**

#### All the goodness

At last we are going to fire up Longhorn’s desktop compositing. Create a new text file and paste the code in "DWM Start' in, save the files as ‘all files’ with ‘bat’ as extension. Run the file and, if the drivers are with you, you may end up with a nice aero enabled 4074. To stop all the goodness (don't know why you would), you can create another bat file with the code in "DWM Stop' to stop it

**Start script**
{{< highlight batchfile >}}
@echo off
rundll32 %systemdrive%\windows\system32\uxdesk.dll,DwmStartComposition
%systemdrive%\windows\i386\sbctl.exe start
tskill explorer
{{< / highlight >}}

The first line of this script isn't strictly needed. I found this to work a bit better than only calling sbctl start directly, but your mileage may vary. The last line restarts the explorer process.

**Stop script**
{{< highlight batchfile >}}
@echo off
rundll32 %systemdrive%\windows\system32\uxdesk.dll,DwmStopComposition
%systemdrive%\windows\i386\sbctl.exe stop
tskill explorer
{{< / highlight >}}

#### Results

If everything went corrent you should end up with something like the picture below. Note that the screenshot also shows the Animated Aurora Preview Pane. More information on how to patch the theme can be found in [another post](/aurora-aero/#fix). You might have also noticed that the borders on all windows are still actually opaque and not the Aero translucent kind. Unfortunately, the original resources are not available in any build. There are, however, a few very good patched theme files with transparency available on the internet as well as a build of 4074 (TWIWMTB) that has a pre-patched theme file.

{{< figure src="4074-dwm-jade.png" title="Aero taskbar and sidebar show up when using an altered version of the Jade theme" >}}