---
title: "4088.lab02_n"
type: build
url: /builds/4088/
build_tag: "6.0.4088.0.Lab02_N.040706-1655"
build_arch: [ "amd64" ]
build_m: 8
install_date: "2004-07-07"
install_key: "TCP8W-T8PQJ-WWRRH-QH76C-99FBW"
---

Leaked 13 January 2015, this is the most recent public Longhorn leak. Although similar to neighbouring builds, it show some minor changes. Before this time only a WinPE build with the same version number was publicly available lacking the install.wim which made installing impossible.

In contrast to [build 4084](/builds/4084/), WinFS is present again. Even though the WinFS services are actually installed there is no way of starting them. You will either get "Error 107:5: The dependency service does not exist or has been marked for deletion" or "Error 1067: The process terminated unexpectedly". Searching will result in a crash of explorer.exe.