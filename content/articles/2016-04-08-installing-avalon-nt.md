---
title: 'Hacking Avalon – 2: Port it'
author: Melcher
type: post
date: 2016-04-08T13:25:55+00:00
url: /installing-avalon-nt
featured_image: /images/avalon-on-xp.png
categories:
  - Hacking Avalon

---
Always wanted to experiment with Avalon on Windows XP? In this second part of the "Hacking Avalon" series we're going to install not only Avalon but also some other Longhorn component. In this post I will take Windows XP as example, but the installer is also compatible with Server 2003.  Below is a description of the included components and their use.

**avalon**

This will install the Longhorn Avalon runtime to your computer. You will be able to run any Avalon application and XAML files compatible with 3683. The Avalon compiler is also included for you to build your own Avalon applications (later more on this in another post).

**sidebar**

Includes all the files needed to display the sidebar. To get the actual sidebar working you will still need to manually patch explorer. Which is something that can't easily be done.

**mygames**

Installs the "My Games" subsystem and file-type declaration for game definition files (GDF). This feature is already pretty much broken in 3683 itself so don't expect too much.

**WinFS**

Installs the WinFS SQL Server.  Since neither Windows XP nor Server 2003 include any user interface for adding metadata to files or for viewing the virtual folders WinFS provides it pretty pointless to use and will mainly be a resource hog.

#### How does the installer work?

Since many features in Longhorn were originally being developer separately from the operating system they were available as component. The component system in early Longhorn builds is the same as the system found in Windows XP and Server 2003. This makes it extremely easy to install a given component on another version of Windows. "Porting" of the component now comes down to copying the right files and creating a bootstrapper for the component wizard. The Windows Component Wizard does all the heavy lifting; renaming files, registering assemblies and so on.

#### Using the installer

Before using the Longhorn feature installer, be sure to install .NET framework version 1. You can download [the redistributable here](https://www.microsoft.com/en-us/download/details.aspx?id=96).

  1. Extract the zip -_Make sure the path to this directory contains no spaces or the installer will break_
  2. Execute _AvalonInstallWrapper_.bat
  3. Wait for the installer to copy some files
  4. A Windows Component Wizard will appear
  5. Select the components you wish to install
  6. When prompted for a directory, point to the _LonghornFiles_ directory in the extracted folder
  7. Wait for the wizard to finish

[3683 feature installer for NT 5.x](/download/3683-feature-installer-nt-5-x.zip)

{{< youtube fA8hya-Qa08 >}}

#### Things to try after installation

Now have your very own Longhornified Windows installation there are some things you definitely have to try:

**Create a XAML file**

XAML files are normally unsupported in Windows XP, but since you just installed Avalon you can open them using Avalon's _shell handler._ Clicking a XAML file will open an Internet Explorer window and render the contents of the file. If your XAML file was empty you will be greeted by an Avalon stacktrace complaining about how empty your file is. The download below contains a valid "hello world' XAML file for you to try.

**The power of WinFS**

Start the "Windows Future Storage' and "Windows File Promotion Manager' services from _services.msc_. WinFS will start indexing files on the file system and drop a ~DirDB file in the root of your main drive. This is the database containing all indexed file on your. Open task manager and see the huge amounts of RAM WinFS is chewing away on while indexing your files.

**Game definitions**

In the zip below you will find a Longhorn game definition file. With mygames installed this file will appear as a game and has some extra options in the right-click context menu.

[3683 feature installer extra files](/download/3683-feature-installer-extra-files.zip)