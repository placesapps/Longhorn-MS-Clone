---
title: "4039.Lab06_n"
type: build
url: /builds/4039-lab06_n/
build_tag: "6.0.4039.Lab06_n.030827-1717, 6.0.4039.Lab06_n.030824-1954"
build_arch: [ "x86" ]
build_m: 6
install_date: "2003-08-28"
install_key: "TCP8W-T8PQJ-WWRRH-QH76C-99FBW"
featured_image: transparent-dce.png
---

This is the first leaked build to use a system in which the complete setup is contained inside the install.wim file. This is also the reason why the image is not bootable: setupldr.bin tries to load the WinPE from a non-exsisting index in the install.wim. A simple workaround is to [start the setup from another build's WinPE](/diskpart/).

Build 4039 is one of only a handful of builds that have the 3D view option in the view menu. Both Panorama and Carousel can be unlocked by adding registry keys, however when Carousel view-mode is chosen no icons will be displayed. Also, this build includes DWM and, when started successfully, adds nice window borders. Explorer tends to render windows very slowly

On January 2020, an earlier yet more unstable compile of this build (`6.0.4039.Lab06_n.030824-1954`, which contains a work-in-progress version of *Visual Studio 2003*, *Product Studio* (a bug tracking tool) and a complete version of *Office 2003* build 5329) was leaked by BetaArchive member grabberslasher.

{{< highlight reg >}}
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer]
"Carousel"=dword:00000001
"Panorama"=dword:00000001
{{< / highlight >}}

### Gallery

{{< gallery third "transparent-dce.png" "plex.png" "opaque-dce.png" >}}