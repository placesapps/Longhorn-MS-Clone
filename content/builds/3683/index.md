---
title: "3683.Lab06_N"
type: build
url: /builds/3683/
build_tag: "6.0.3683.0.Lab06_N.020923-1821"
build_arch: [ "x86" ]
build_m: 3
install_date: "2002-09-24"
install_key: "CKY24-Q8QRH-X3KMR-C6BCY-T847Y"
featured_image: overview.png
---

3683.Lab06_N was the first Codename "Longhorn" build to leak publicly on the internet. It was leaked on 20th October 2002 by the xBetas release group. The publicly leaked version is a modified Professional x86 release, featuring xBetas branding. Some private collectors have an untouched copy of the release.

Despite being the earliest build available, it debuts a number of features new to Longhorn and even includes a few that do not exist in later builds. The "Avalon" extension to the .NET Framework makes its first appearance within this build, and uniquely is built on top of a released .NET version (v1.0) instead of the in-development versions found in later builds (either v1.2 or v2.0 pre-release). This quirk allows you to [transplant the version of Avalon](/installing-avalon-nt/) in 3683 onto Windows XP.

It is one of only two builds to include a new [display display panel](/avalon-display-panel/) enabled out of the box - the other is [4093](/builds/4093/), which featured an entirely redeveloped display control panel. Other Milestone 3 builds included the same display control panel as 3683, but it is locked behind a registry key and is progressively more and more broken with each passing build up to its removal shortly after the start of Milestone 4.

Under the hood, the system is also being moved over to a [new branding API](/pig-latin/) that would consolidate branding from different components all over the system into one single, common API. There's also a small amount of early prototype code for the [Start page](/startpage/), though this is not exposed out of the box.

Lastly, the build contains the [Desktop Compositing Engine](/desktop-compositing/), though there is no UI to control it yet. It also does not work under virtual machines due to a compatibility issue with the emulated GPUs that they use.

### Gallery

{{< gallery 25 "desktop.png" "explorer.png" "overview.png" "contacts-browser.png" >}}

### Related Articles

* [Tips and tricks for this build](/3683-tips-tricks/)
* [Compiling XAML in 3683](/avalon-compiling-it/)