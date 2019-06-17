---
title: My TV and Movies
author: Melcher
type: post
date: 2014-10-25T20:17:03+00:00
url: /my-tv-and-movies
featured_image: mytv-guide.png
categories:
  - Research

---
The My TV and Movies _library_ becomes visible when using the Media Center Edition (_Freestyle_) variant of some Longhorn builds. The My TV and Movies library is a media application for recording and watching TV. The application is an Avalon container and is opened in Internet Explorer by the Avalon Shell Handler. The container itself includes a couple of dll and BAML files as well as a manifest.

{{< gallery 50 "mytv-3718.png" "mytv-guide.png" >}}

In some builds the filesize is noticeably bigger because it includes placeholder images. Although there is also a placeholder image for the guide, this page will always throw an error when clicked. A placeholder for "Watch Live TV" is also included, but the page will just show up empty. In a later version of MyTVapp found in 4008 and 4015, the application will throw an exception.

{{< gallery 50 "mytv-3706.png" "mytv-4008.png" >}}

To open the application run `C:\Windows\System32\mytvapp.container` or convert Longhorn from Professional to Media Center Edition. This application is present in builds: 3706, 3713, 3718, 4001, 4008, 4015 and 4029.