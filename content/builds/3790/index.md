---
title: "3790.winmain"
type: build
url: /builds/3790/
build_tag: "5.2.3790.1232.winmain.040819-1629"
build_arch: [ "x86" ]
build_m: "Omega-13"
install_date: "2004-08-20"
install_key: "CKY24-Q8QRH-X3KMR-C6BCY-T847Y"
---

Built only hours after [build 4093](/builds/4093), this is the first build form the main branch after the reset. Note that the main branch has been renamed to winmain. This build identifies itself as being Longhorn in the _End User License Agreement_. General consensus is, however, that 3790 isn't a Longhorn build at all. It rather is a main branch compilation of the Server 2003 SP1 RC codebase. This build was likely only compiled as a known-good baseline with which to test the new build systems that had been put in place after the reset. Actual development had already begun in a [virtual build lab](/vbl/), compiling a series of builds with the number 5000, from which development continued.

During setup you will be asked to locate some missing files. All of the missing files are in the i386 directory on the installation media. Because of the nature of this build, setup doesn't know where to look for the files itself. After installation this build requires you to activate Windows immediately. To bypass activation boot into safe-mode an apply your favourite activation crack.