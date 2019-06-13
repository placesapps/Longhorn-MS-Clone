---
title: Diskpart
author: Melcher
type: post
date: 2014-10-25T16:33:28+00:00
url: /diskpart
featured_image: /images/longhorn-setup.png
categories:
  - Tutorials

---
Diskpart is a command line tool that'll let you manage disks in Windows. Diskpart comes in more than handy when installing Longhorn since numerous Longhorn WinPEs have trouble formatting disks themselves. On this page you will find a brief description on how to use this tool to partition a disk for installing Longhorn and a little extra.

In any WinPE press Shift + F10. This will bring up a command prompt window. In this window type: `diskpart`, now diskpart will initialize. To partition a disk execute the following commands line by line.

```
select disk 0
clean
create partition primary
select partition 1
active
assign
exit
```

You now have created a partition on disk 0 which is assigned a drive letter and is active. If there are multiple drives in the system be sure to select the correct disk. For a list of disks you can type `list disk`.

![](/images/lazy-diskpart-session.png)

![](/images/diskpart-session.png)

#### Formatting

Sometimes it's not enough to just partition the drive. A couple of Longhorn installers also have trouble formatting the drive. You can manually format a drive by executing:

```
format fs=ntfs quick
```

In the example above the drive you selected before (drive 0) gets quick formatted with the NTFS file-system.

#### Executing setup from WinPE

If the Longhorn image doesn't boot at all, it's also possible to complete above steps and start the Longhorn setup from a WinPE that's on another image. To do this in a VM, just add an additional CD/DVD drive and mount any Windows installation disc that uses WinPE (I mostly use a Windows 7 disc for this). Mount the Longhorn image to the other disc and make sure the VM boots from the alternative disc (so, Windows 7 in my case). When the WinPE is loaded, simply press Shift + F10 and diskpart away! To start the Longhorn setup navigate to the correct drive in command prompt (`X:`, probably it's drive E) and execute `setup`. The Longhorn setup will commence!

{{< figure src="/images/longhorn-setup.png" title="Longhorn setup started from Windows 7 WinPE" >}}