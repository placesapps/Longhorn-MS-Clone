---
title: "4084.main"
type: build
url: /builds/4084
build_tag: "6.0.4084.0.main.040527-0915"
build_arch: [ "x86" ]
build_m: 8
install_date: "2004-05-28"
install_key: "TCP8W-T8PQJ-WWRRH-QH76C-99FBW"
---

Very empty build, most interesting features had been removed by this time to implement them again one by one over time. WinFS has been cut in this build. None of the required services is present after installation, even the libraries are gone from Computer.

### Fixes
The setup fails to format the disc before copying files which always results in a "An error occurred while preparing the install drive" exception. This error is causd by a missing dll in the WinPE sector of the install.wim, _vssapi.dll_. An easy workaround is to [partition and format the drive from another build's WinPE](/diskpart).

After the first stage you will need to edit `C:\Windows\System32\onlinesetup.cmd`. Remove the lines listed beneath.

```
if errorlevel 1 (
     echo Error in running setup.exe
     pause
     goto :DoInstall
)
```

If you fail to remove above lines from the file, the setup will end up in an endless loop. Removing the lines will make the setup finish no matter if there was an error.