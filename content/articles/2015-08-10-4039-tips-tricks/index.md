---
title: '4039 Tips & tricks'
author: Melcher
type: post
date: 2015-08-10T11:53:14+00:00
url: /4039-tips-tricks
categories:
  - 'Tips & tricks'

---
This is the very first page in its kind; a tips 'n tricks page. More of these pages will follow for other interesting builds, showing you the ins and outs and providing easy tutorials to activate hidden features. Pages like this will be updated every so often to include the latest finds. But for now, 4039.

#### Enable Aero glass {#aero-glass}

This build contains some super sleek Aero glass resources in desksrv.dll for the theming service to use. By default, the opaque resources will be used, but a simple patch of desksrv.dll enables the glass borders on windows when DCE is running. For a tutorial on how to enable DCE please see [this page](/desktop-compositing). The desksrv patch involves simply replacing the opaque PNG files with the transparent ones. While this is neat and all, it's not a very original way of doing things. Luckily there is a much more convenient and original trick to enable transparent borders.

1. Browse to the themes folder, C:\Windows\Resources\Themes\
2. Copy the Plex folder and rename it to Aero.
3. Rename the plex.msstyles file inside the folder to aero.msstyles.
4. Open up commandprompt and enter 
  {{< highlight batchfile >}}
  net stop winux
  net start winux
{{< / highlight >}}
  These commands will consecutively stop and start the theming service. This needs to be done since the service looks for the aero.msstyles file on startup only. If the file was found, Aero glass is enabled.
    
5. Now start DCE by executing `C:\Windows\i386\sbctl start`

{{< youtube 9JfT4quE3Cg >}}