---
title: Out-of-box experience
author: Melcher
type: post
date: 2014-11-06T13:06:36+00:00
url: /oobe/
featured_image: 1.png
categories:
  - Features

---
With the new image-based installation introduced in Milestone 4 it was also time for a revamped out-of-box experience (OOBE) wizard. The first build to feature the image-based install and new OOBE wizard is [build 4001](/guide/4001/).

After a brief time loading at the "Please wait&#8230;' page you will find yourself at the _WelcomePage_ where you will be welcomed to the wizard. On the next page, _aacnamepage_, you can add as many users as you like. After doing this, you will find yourself at _FinishPage_. Even though this really is the end of the setup, the text on the page suggests that the setup continous after this page:

> As Setup continues, you can personalize your computer by selecting background pictures, colors, and user tiles.

The four pages of the wizard in build 4001.

{{< gallery 25 "1.png" "2.png" "3.png" "4.png" >}}

After installation the files can be found in the `C:\Windows\System32\oobe\` directory. In most builds this folder also still contains the XP-style OOBE wizard in html. The new oobe wizard is composed of the following files:

* **background.jpg, button.jpg**

	Obviously the background and button images used by the wizard. Both files have a low quality couterpart with a _low suffix.

* **ooberes.dll and ooberesl.dll** 

	Each of these files holds the complete base-set of XAML files for every wizard page. Ooberesl, however, uses the lower quality images. A function determines what version of the dll is used.

* **oobeui.dll**

	Contains all the working code for each page in the wizard, including click events etc.

* **spuilib.dll**

	Contains elements that are used in the XAML code.

* **setup.exe**

	Supposed to start the oobe wizard.

All builds except 4084 and 4093 (and x64 builds) have an OOBE wizard consisting of above files. It is interesting to note that setup.exe in 4001 and 4011 contains a green version of the background found in the oobe folder. I replaced the original blue background with the green one, see the images below for an impression. As of build 4051, setup.exe contains a Slate style background.

{{< gallery 25 "green2.png" "green1.png" >}}

OEM configurability was also introduced in build 4051. At start of the wizard, oobeui will always check for the OEMUI.xml configuration file. Via this config file OEMs would have been able to add and/or replace pages in the wizard. Extra pages were to be loaded from another assembly (specified in the config file) using System.Reflection. Using the code in oobeui hounsell re-created the lay-out of such a config file.

{{< highlight xml >}}
<?xml version="1.0"?>
<Wizard xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<OEMAdd>
		<WizardPageData>
			<Assembly>TestAssembly</Assembly>
			<NameSpace>TestNamespace</NameSpace>
			<WizardPage>TestWizardPage</WizardPage>
		</WizardPageData>
	</OEMAdd>
	<RegAdd>
		<WizardPageData>
			<Assembly>TestAssembly</Assembly>
			<NameSpace>TestNamespace</NameSpace>
			<WizardPage>TestWizardPage</WizardPage>
		</WizardPageData>
	</RegAdd>
	<RegReplace>
		<WizardPageData>
			<Assembly>TestAssembly</Assembly>
			<NameSpace>TestNamespace</NameSpace>
			<WizardPage>TestWizardPage</WizardPage>
		</WizardPageData>
	</RegReplace>
</Wizard>
{{< / highlight >}}

The ooberes and ooberesl contain more pages than shown during the actual wizard. The extra pages _netdetectpage_ and _networkpage_ are present, but no code for these pages can be found in oobeui.dll. In later builds another page hidden page can be found, called _registrationpage_.

{{< gallery 25 "5.png" "6.png" "7.png" >}}

##### Special thanks to Ultrawindows