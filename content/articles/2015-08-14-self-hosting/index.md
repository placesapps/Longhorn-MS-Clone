---
title: Self-hosting
author: Melcher
type: post
date: 2015-08-14T14:12:22+00:00
url: /self-hosting/
featured_image: 4042votenow.png

categories:
  - Features
  - History

---
At Microsoft, it is common practice to use products still under development to continue development of that very product. Once a stable version of a product is available, developers are encouraged to install it on their workstations and use it for every day use. Developers using the product can directly provide feedback and report bugs to teams working on certain features.  This process is internally called _self-hosting_. Often times the process is also referred to as "eating your own dog food" or _doogfooding_: when the product is no good and tastes nothing better than dog food, developers will still need to _eat_ it.

The idea of self-hosting is to quickly get feedback and bug reports as mentioned earlier. Another reason to do this is also to keep in touch with the product. Since developers actually have to use their product, they see and experience what end users of the final product will see.

The "VoteNow" application found in Longhorn builds 4033, 4039, 4042, 4053, 4084 and 4093 is part of the self-hosting program during Longhorn development. VoteNow enables the user of a build to cast a vote for the current build on the internal Longhorn's project site. Even though VoteNow is configured to run at startup of each of the above builds you normally won't notice it because it automatically closes itself as soon as it's launched. After some research, it became clear VoteNow runs a series of checks to make sure the current user is indeed a Microsoft employee and is allowed to cast a vote. When the requirements are not met the application will simply exit.

### IsLegalVoter?

The first check is implemented by the method IsLegalVoter(). This method verifies if the current userdomain environment variable if a known Microsoft domain. Valid domains:

```
NTDEV, WINDEPLOY, REDMOND, SEGROUP, XRED, XCORP, CORP, WINSE, 
INTERACTIVE, WINGROUP, SYS-WINGROUP, PHX, AFRICA, EUROPE,
MIDDLEEAST, NOTRHAMERICA, SOURTHAMERICA, SOUTHPACIFIC
```

### Labs

The next check only takes place after a timer lasting 4 hours has elapsed. This check looks for the current build's lab. Recognized virtual build labs include the widely known labs 1, 2, 3, 4, 5 (main), 6 and 7 but also 21. The exact purpose of lab 21 remains unknown. Any unrecognized lab returns the value "BadLab" and the application closes.

### VoteNow toast

A toast notification appears after all of the above checks and another timer have been passed. The notification offers three options:

* Vote Now - opens up Internet Explorer and navigates to the internal voting page for the current build. For build 4033 the URL would look like `http://winweb/selfhost2/?ballot=3&lab=main&build=4033.030717`.
* Later - resets the application
* Learn more - opens up Internet Explorer and navigates to the general self-hosting page `http://longhorn/selfhost/`

{{< gallery 50 "4042votenow.png" "4042votenowcollapsed.png" >}}

I have re-created the VoteNow application using the orignal code and omitted the checks. The video below shows this application in action.

<video width="100%" preload="metadata" controls="controls">
  <source type="video/mp4" src="4033-self-host-toast.mp4" />
  <a href="4033-self-host-toast.mp4">Download video</a>
</video>

[4033 Vote Right Now](/download/4033-vote-right-now.zip)

##### Thanks to UltraWindows for helping me understand VoteNow