---
title: "4033.main"
type: build
url: /builds/4033-main
build_tag: "6.0.4033.0.main.030717-1555"
build_arch: [ "x86" ]
build_m: 6
install_date: "2003-07-18"
install_key: "TCP8W-T8PQJ-WWRRH-QH76C-99FBW"
featured_image: desktop.png
---

The publicly available image of this build has had its pidgen.dll replaced. This means that the orignal product key as listed above does not work. Instead, you will need to enter the key `QW32K-48T2T-3D2PJ-DXBWY-C6WRJ`. If you would like to use the original key, you can replace the unauthentic pidgen.dll (origination from Server 2003 RTM) in the Sources directory with the original file that's for download below.

[Pidgen from 4033](/download/pidgen.zip)

During setup be sure to select Disk 0. Otherwise, the setup will always state the disk does not have sufficient drive space.

This build is one of the few builds that have a 3D view option in explorer. Applying the registry key below will add additional view modes. Viewing files in explorer with the 3D view-mode is heavily broken in this build. Enabling DCE is also possible in this build.

{{< highlight reg >}}
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer]
"Carousel"=dword:00000001
"Panorama"=dword:00000001
{{< / highlight >}}

### Gallery

{{< gallery 25 "desktop.png" "explorer.png" "carousel.png" "panorama.png" >}}