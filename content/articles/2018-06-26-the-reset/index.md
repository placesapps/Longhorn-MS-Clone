---
title: The reset
author: Melcher
type: post
date: 2018-06-26T22:25:14+00:00
url: /the-reset
featured_image: 4042-2014-11-17-14-34-01.png
categories:
  - History

---
The piece of text you read below was originally part of the "[Guide](/builds)" section present on the very first iteration of the "Experience Longhorn" site. Since the switch to WordPress as a CMS and all changes to the theme there has been no more place to have it on what is now called the [Builds list](/builds). I really didn't want to throw the story on the reset away though, so here you have it: a short an concise explanation about the infamous Longhorn reset.

The newest Windows product at the time of the reset in late 2004 was Windows Server 2003 sp1 RC, which was used as a base after the reset. The new codebase was first componentised before any new features were added to it. Work on componentising the Server 2003 codebase had already begun weeks before build 4093 was compiled. The post-reset range started at build 5000. The first post-reset builds were compiled by the [vbl_core](/builds/branch/base/vbl_core) lab. The last pre-reset build compiled probably is 4094.private/Lab06\_dev\_tech(skatari).

### When did this happen?

As described above post and pre-reset builds were compiled side-by-side. The reason of these builds being compiled side-by-side probably is that the developers still tried to save the pre-reset Longhorn, but really all hope was lost and other labs were already tasked with compiling builds based on the newer Server 2003 codebase.
  
Because of this situation it's hard to pin-point an exact date at which the reset took place.
  
Some sources say that at the time of WinHEC 2004 (May 2004) Microsoft executives already knew that Longhorn wasn't going to work in it's current form and that a reset would be necessary. A memo by Jim Allchin (Vice president back then) sent 7 January 2004 reveals that Longhorn was already in trouble at that time; "LH is a pig and I don’t see any solution to this problem." ([full memo here](http://blog.seattlepi.com/microsoft/2007/01/10/jim-allchins-mac-message-the-full-text/)) The Wall Street Journal later revealed that in July 2004 Jim Allchin contacted Bill Gates and said that Longhorn was terribly behind schedule and was not going to make it. The first post-reset builds got compiled the next month.

### Why start over?

One of the reasons of the reset most likely is the .NET framework. The .NET framework was fairly new at the time the Longhorn project started. Initially, Longhorn's successor, Blackcomb, was to be stuffed with .NET code, but later on it was decided that Longhorn was to include lots and lots of .NET stuff. Basically all of the user interface visuals where programmed in .NET through the new Avalon API; sidebar, preview pane etc. At last, it became clear that the still immature .NET framework simply was not up to the job of driving the complete UI. Moreover, dependencies between managed .NET code and unmanaged code became so complicated that the code became unmanageable. Ultimately, Longhorn became a big, bulky thing which was a step back from XP in reliability and security.

### What changed?

For a start, Longhorn was now based on the newer Server 2003 sp1 RC codebase. Before this point it had been based on Server 2003 RC code and possibly even earlier versions of Server 2003. The build lab system was overhauled and renamed to virtual build labs. Measures were taken to make sure no bug-filled code could be reverse-integrated into the main branch, which was now called winmain. Furthermore, componentising of features was now done before they were added instead of first adding all features and componentising afterwards. Robert Scoble, programmer in the Longhorn days, stated that it was also prohibited to write in .NET after the reset. All new code had to be written in C++. It looks like the Vista Media Center is the only exception to this rule.

### Still Longhorn?

There is much debate as to whether or not it's appropriate to call builds compiled after the reset "Longhorn' still. Since the final product name, Vista, was only announced at 22 July 2005 we believe it's appropriate to call all builds compiled before that date still Longhorn. We decided to list builds up to the 53xx range in the guide because any later builds, in our eyes, bear too much resemblance with Vista to still call them Longhorn.

### Omega-13

The name Omega-13 is used to describe the phase directly after the reset. Omega-13 is a reference to the Galaxy Quest TV show. In this series the Omega-13 device permits the user as 13 second time jump to the past to correct a single mistake.