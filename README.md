# msi-gs75-stealth-howto
Tips and tricks to build, configure, and optimize my MSI GS75 Stealth Laptop

# Why
The MSI GS75 Stealth is a tricky beast to rebuild from scratch and get working properly. It has a ton if required drivers, utilities, and configurations. An improper/incomplete build could lead to problems with cooling, connectivity, keyboard/touchpad, peripherals, and more. Unfortunately, MSI does not provide a one touch install to rebuild the laptop as if it just shipped from the factory.

This page outlines how to build the MSI GS75 Stealth from scratch. This includes things like installing the OS, drivers, utilities, and patches; creating backups; configuring and tweaking settings; list of cool apps and addons; and more.

# Hardware

| Overview  | Part # / Spec Sheet    | Support | User Manual |
|  ---  |  :-:  |  :-:  |  :-:  |
| [MSI GS75 Stealth 17.3" Full HD 300Hz Gaming Notebook Computer, Intel Core i9-10980HK 2.4GHz, 32GB RAM, 1TB SSD, NVIDIA GeForce RTX2070 Super Max-Q 8GB, Windows 10 Pro](https://us.msi.com/Laptop/GS75-Stealth-10SX/Overview) | [GS75 Stealth 10SFS-028](https://storage-asset.msi.com/specSheet/us/nb/GS75%20Stealth%2010SFS-028.pdf) | [Link](https://us.msi.com/Laptop/GS75-Stealth-10SX/support?sku_id=79435) | [Link](https://download.msi.com/archive/mnu_exe/nb/G_MS-17G3_v1.0_English.pdf)

# OS, Drivers, & Utilities
This section outlines how to get Windows 11 and all the drivers and utilities installed and working properly. This is the bare minimum required to configure this laptop.

TIP: Save everything you download in this section to a backup location (ex. USB drive, second hard drive, etc). This will come in handy if you ever need to rebuild and the download links are not accessible (maybe you have no/poor internet, maybe the link was pulled, etc).

## OS
* Create your Windows 11 installation media: https://support.microsoft.com/en-us/windows/create-installation-media-for-windows-99a58364-8c02-206f-aa6f-40c3b507420d
* When the install begins, delete all partitions
* Complete the OS install
* Do not install any Windows updates until after completing the driver & utility installs

## Drivers
Installing drivers directly from MSI ensures your laptop functions like the day you bought it (I once rebuilt my laptop solely using drivers from Windows update and ran into issues like the display being locked at 64hz as opposed to its true 300hz). After installing drivers from MSI, you can use Windows updates to help keep your drivers up to date.
* Go to the support page (linked in the Hardware section above) and then download/install every driver (in the order listed on the page)

## Utilities
Utilities are just as important as drivers. They include needed functionality, needed interfaces, and sometimes needed drivers.
* Go to the support page (linked in the Hardware section above) and then download/install every utility (in the order listed on the page) with the following exceptions:
  * Do not install the Intel Graphics Control Panel (it has been retired). Instead install the [Intel® Graphics Command Center](https://www.microsoft.com/en-us/p/intel-graphics-command-center/9plfnlnt3g5g?activetab=pivot:overviewtab).
  * Do not install SteelSeries Engine (it has been retired). Instead install [SteelSeries GG](https://steelseries.com/gg).
  * Install True Color 4.0 instead of 3.0
  * Do not install GeForce Experience from MSI. Install from [here](https://www.nvidia.com/en-us/geforce/geforce-experience/download/).
  * Do not install Dragon Center until reading the below:
    * **NOT RECOMMENDED:** The latest versions from MSI and the MS App store seems to have a bug where the fan speed curves in a User scenario don't work (causing my laptop to overheat and shutdown).   
    * **RECOMMENDED:** [Dragon Center 2.0.108](https://download.msi.com/uti_exe/mb/Dragon_Center_2.0.108.0.zip) works perfectly for me (and I wouldn't update it further). It has all the looks, features, and functionality of the latest version.

    * **ALTERNATIVE:** [Dragon Center 1.2.1709](http://download.msi.com/uti_exe/nb/DragonCenterv1.2.1709.1101_1.2.1709.1101_0x2cfac57f.zip) also works perfectly, has the benefit of being able to create 5 user scenarios with hotkeys and more (great if you really need to customize), but uses the old Dragon Center interface and has reduced functionality (ex. no monitoring of individual fan speeds).

## Peripherals
Connect any peripherals (ex. printers, keyboard/mouse, dock/hub, etc), install drivers/utilities, and validate they work as expected.

## Recovery
* Create a restore point (ex. name = Windows 11, All drivers & utilities installed)
* Create a [system image](https://answers.microsoft.com/en-us/windows/forum/all/how-to-create-a-system-image-in-windows-11-and/036110b8-66bb-4cc7-b9e2-2d66df27d236)
  
# Temperature Control
This laptop gets crazy hot to the point where games will be throttled, fan noise and physically touching the laptop will be unbearable, and even to where the laptop abruptly powers off. My main strategy to combat this (bringing the idle temp down from 75 to 55 and keeping high frame rates and preventing abrupt shutdowns - while also elongating battery life) is below, in order of most effective/safest/easiest to implement to riskier/harder to implement:
* Disable Turbo
* Power Plan
* User Scenarios
* Gaming Mode
* Disable Unwanted Startup Applications
* Cleaning and Clearing Fans
* Laptop Cooler
* Undervolting
* New Paste & Pads

## Disable Turbo
Turbo is a feature where your CPU's base frequency can be boosted to its maximum turbo frequency. While this gives you more processor performance, it also draws more power and generates more heat. You're going to see people arguing on whether this is a good idea or not. You paid for a high performing processor, just to throttle it?  Well, if your laptop is heating up to the point where the processor is throttling anyway, other methods do not provide as good a way of reducing temps, and you don't perceive the performance difference - then its OK in my book to disable turbo. Disabling Turbo provided me with the highest drop in temperature with no perceived impact in performance. You can disable turbo in 2 ways - BIOS setting and or ThrottleStop. Disabling in the BIOS is my preference as it is disabled immediately after BIOS loading and doesn't depend on ThrottleStop being installed, configured, and working.

To disable turbo in the BIOS:
  * Restart your laptop and press the delete key to enter the BIOS
  * Press right shift + right Ctrl + left alt + f2 to enable hidden BIOS settings
  * Advanced > Power & Performance > CPU – Power Management Control 
  * Set Turbo to Disabled
  * Exit & Save

## Power Plan
  * Choose the "Balanced" plan
  * Edit the plan
    * Processor Power Management
      * Min on battery: 5%
      * Min plugged in: 50%
      * Max on battery: 90%
      * Max plugged in: 90%

## User Scenarios
Using the Dragon Center 2.x user scenarios I typically configure and switch between the following:
* Extreme Performance (used when gaming or when I need to cool the laptop down quickly - fans run loud and at max)
  * Edit and ensure Cooler Boost is checked
* User (used when I'm not gaming - fans are quiet but ramp up when the laptop heats up)
  * Edit and set:
    * Performance level to medium
    * Fan speed to advanced, click the gear next to "advanced", and set:
      * CPU: 0%, 0%, 0%, 40%, 65%, 150% (this will keep the fans silent/off until the laptop hits 65)
      * GPU: 0%, 50%, 60%, 75%, 90%, 150%

### Understanding the Fan Curves
When setting the fan curves in the User Scenario | Fan Speed | Advanced, there are no indicators to understand temperature and no explanation of speed (especially since values for 3 fans add up to 150%). Here's my understanding after experimenting:

#### Speed
* Values 0-100% control fans 1 and 2
* Values above 100% control fan 3

Examples: 
* A value of 150% sets all 3 fans to 100%
* A value of 125% sets fans 1 and 2 to 100% but sets fan 3 to 50%.
* A value of 100% sets fans 1 and 2 to 100% but turns off fan 3
* A value less than 100%, sets fans 1 and 2 to that value but turns off fan 3

#### Temperature
1) < 50 degrees
2) Kicks in at 50, then turns off at 45
3) Kicks in at 60, turns off at 65
4) Kicks in at 65, turns off at 60
5) Kicks in at 70, turns off at 65
6) Kicks in above ?, turns off at ?

## Gaming Mode
Gaming Mode in Dragon Center allows you to automatically run all 3 fans at 100% when specific programs are ran. This is a great way to ensure your laptop stays cool and stable while gaming.
*  Add every game / high performance application to Gaming Mode

### Tips
* For games, try to add the game executable as opposed to any startup executables. 
  * Ex. Batman Arkham Asylum has a startup executable BmStartApp.exe that launches a menu startup executable BmLauncher.exe that loads the game executable ShippingPC-BmGame.exe when you click the "Play" menu option. Here you would add the game executable ShippingPC-BmGame.exe to Gaming Mode.
* For steam games, most game executables have "shipping" in the name.
* I have not figured out how to add game executables from Xbox Game Pass

## Disable Unwanted Startup Applications
The more startup applications that run, the harder your system works, the hotter your laptop gets. So the goal here is to have your laptop only run the startup applications you need. You can learn how to disable startup applications [here](https://www.groovypost.com/howto/disable-startup-apps-on-windows-11/). These are the startup applications I disable (which may or may not be present on your laptop):
* Cortana
* Any utilities for your scanners or printers
* Logitech Download Assistant
* Microsoft Edge
* Spotify
* windows Terminal
* Xbox App Services
* iCloud *

## Cleaning and Clearing Fans
After a while, you're fans will get clogged with dirt, dust, and grime. This will affect their ability to cool. To clean them, turn the laptop off, blow them out with compressed air, and use a alcohol dipped q-tip to manually clean the blades.

You should also ensure your fans are clear to blow out air. For example, placing your laptop directly on your lap or on a pillow may cause the fans to be blocked. Use a laptop tray anr or a laptop cooler (see next section).

## Laptop Cooler
If your built in fans are good enough, use more fans. A USB laptop cooler is a cheap, easy way to bring your temps down a few degrees. This is the one I use:
https://www.amazon.com/gp/product/B00NNMB3KS/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1

## Undervolting
Undervolting provides reduced electricity to your CPU, CPU Cache, GPU, etc than it normally calls for, thus reducing power usage and temp. The problem is determining what values you can set that won't freeze or crash your system. Theres a whole art to this but here's what I did:
* Unlock in the BIOS to allow undervolting
  * Restart your laptop and press  delete to enter the BIOS
  * Press right shift + right Ctrl + left alt + f2 to enable hidden BIOS settings
  * Advanced > Power & Performance > CPU – Power Management Control > View/Configure CPU Lock Options, set CFG Lock to disables, and save/exit
* Install and configure [ThrottleStop](https://www.techpowerup.com/download/techpowerup-throttlestop/):
  * Open Options and check Start Minimized, Minimize on Close, and Nvidia GPU
  * Open FIVR and set:
    * CPU Core Offset Voltage: -200 mV
    * CPU Cache Offset Voltage: -100 mV
  * Test your system and apps to ensure they run stable. Reboot and re-test. Adjust as necessary and reboot/re-test.
  * Create a [scheduled task to start ThrottleStop at startup](https://www.repairwin.com/how-to-start-throttlestop-at-windows-startup/)

## New Paste and Pads
Thermal paste and pads are a way to efficiently transfer heat from your core components like CPU/GPU to a heatsink. The better the paste/paste job/pads, the better the heat transfer and the cooler your system will be. This has become so popular and helped so many people that resellers now offer this an an option when buying gaming laptops (because the factory paste/padding may be subpar). The process to do this is quite involved though and won't be outlined here. I have only repasted and noticed minimal temp differences (5-10 degrees). Maybe one day I'll re-paste (maybe with liquid metal), apply new pads, see a different result, and update this section.

# Tweaks
| Name      | Description      | Notes |
| --- | --- | --- |
| [O&O ShutUp10++](https://www.oo-software.com/en/shutup10) | O&O ShutUp10++ means you have full control over which comfort functions under Windows 10 and Windows 11 you wish to use, and you decide when the passing on of your data goes too far. Using a very simple interface, you decide how Windows 10 and Windows 11 should respect your privacy by deciding which unwanted functions should be deactivated. | This will help protect your privacy and well as reduce the load on your laptop and network. *Apply recommended settings - EXCEPT FOR Location Services | Disable Functionality to locate the system (if you enable this, you will not be able to find your laptop using the Find My Device feature) * |
| [Windows10Debloater](https://github.com/jstnlth/Windows10Debloater/tree/addWhitelistDefaults)| Script/Utility/Application to debloat Windows 10/11, to remove Windows pre-installed unnecessary applications, stop some telemetry functions, stop Cortana from being used as your Search Index, disable unnecessary scheduled tasks, and more. | This will help protect your privacy and well as reduce the load on your laptop and network. *Run the GUI script and select to remove all bloatware*|
| [MSI Wallpaper](https://cutewallpaper.org/download.php?file=/21/msi-wallpaper/MSI-Gaming-Wallpaper-1920x1080-on-MarkInternational.info.jpg)|This wallpaper includes a dark, detailed MSI dragon logo.|*Set you desktop and lock screen wallpaper* |
| [Set a custom New Tab Page in Microsoft Edge](https://answers.microsoft.com/en-us/microsoftedge/forum/all/how-to-set-a-custom-new-tab-page-in-microsoft-edge/af0590f8-9a5c-46c5-bd25-5150aed60d8c?auth=1) | Microsoft Edge has options to set or change the page(s) that open when the browser is launched (Note 3), and also to set a home page accessed by clicking the Home button Image next to the address bar (Note 4). However, a new tab will always open to the browser's own New Tab Page. If you would rather have a different page in new tabs, this article explains how to do it. |*Use this to control what page appears when opening a new tab.*|

# Finish
* Scan your system with [Norton Power Eraser](https://support.norton.com/sp/en/us/home/current/solutions/kb20100824120155EN)
  * While Windows 11 includes Windows Defender, this is quick, easy way to double check that your system is clean.
## Recovery
* Create a restore point (ex. name = Windows 11, All tweaks, configurations, tools, and apps)
* Create a [system image](https://answers.microsoft.com/en-us/windows/forum/all/how-to-create-a-system-image-in-windows-11-and/036110b8-66bb-4cc7-b9e2-2d66df27d236)

# Personal
From here down, we are no longer talking about building the GS75 Stealth laptop but are talking about personalizing a laptop to my specific likings. This includes additional steps, configurations, and apps to customize my laptop for me. This may or may not be desirable or applicable to you - take a peek and apply what you want. 

## Configurations
* Set the correct time zone
  * Powershell example: `Set-TimeZone -Name "Eastern Standard Time"`
* Sign-in options
  * Set a PIN
  * Configure Facial Recognition

## Making your laptop more Mac like
* [iCloud for Windows](https://support.apple.com/en-us/HT204283)
  * Browser - Bookmarks:
    * Install chrome (needed to turn on syncing, even if you just use edge)
    * Install and enable [iCloud Bookmarks](https://chrome.google.com/webstore/detail/icloud-bookmarks/fkepacicchenbjecpbpbclokcabebhah?hl=en)
  * Browser - Passwords
    * [iCloud Passwords](https://chrome.google.com/webstore/detail/icloud-passwords/pejdijmoenmkgeppbflobdenhhabjlaj?hl=en)
* [Blue Bubbles](https://bluebubbles.app/)
* [iTunes](https://support.apple.com/en-us/HT210384)

## Developer Tools
| Name      | Description      | Notes |
| --- | --- | --- |
| [Git for Windows](https://gitforwindows.org/)      | Git for Windows focuses on offering a lightweight, native set of tools that bring the full feature set of the Git SCM to Windows while providing appropriate user interfaces for experienced Git users and novices alike.     ||
| [Visual Studio Code](https://code.visualstudio.com/download)|Visual Studio Code is a source-code editor made by Microsoft for Windows, Linux and macOS. Features include support for debugging, syntax highlighting, intelligent code completion, snippets, code refactoring, and embedded Git|Install if you regularly edit code or use Git|

### Visual Studio Code Extensions
| Name      | Description      |
| --- | --- |
| [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) | A basic spell checker that works well with camelCase code. |
| [Auto-Open Markdown Preview](https://marketplace.visualstudio.com/items?itemName=hnw.vscode-auto-open-markdown-preview) | Open Markdown preview automatically when opening a Markdown file |
| [Block Sort](https://marketplace.visualstudio.com/items?itemName=1nVitr0.blocksort) | Sort Blocks instead of lines! Works for all major programming languages including JavaScript / TypeScript, Java, JSON, XML, etc. |
| [Bracket Pair Colorizer 2](https://marketplace.visualstudio.com/items?itemName=CoenraadS.bracket-pair-colorizer-2) | A customizable extension for colorizing matching brackets |
| [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker) | Makes it easy to create, manage, and debug containerized applications. |
| [gitignore](https://marketplace.visualstudio.com/items?itemName=codezombiech.gitignore) | Lets you pull .gitignore templates from the https://github.com/github/gitignore repository. Language support for .gitignore files. |
| [GitLens — Git supercharged](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) | Supercharge the Git capabilities built into Visual Studio Code — Visualize code authorship at a glance via Git blame annotations and code lens, seamlessly navigate and explore Git repositories, gain valuable insights via powerful comparison commands, and so much more |
| [Auto-Open Markdown Preview](https://marketplace.visualstudio.com/items?itemName=hnw.vscode-auto-open-markdown-preview) |Open Markdown preview automatically when opening a Markdown file|
| [Markdown Preview Github Styling](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-preview-github-styles) | Changes VS Code's built-in markdown preview to match GitHub's styling.|
| [Markdown Table Generator](https://marketplace.visualstudio.com/items?itemName=JayFiDev.tablegenerator)|Generate formatted tables for markdown|
|[PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell)|Develop PowerShell modules, commands and scripts in Visual Studio Code!|
|[Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)|IntelliSense (Pylance), Linting, Debugging (multi-threaded, remote), Jupyter Notebooks, code formatting, refactoring, unit tests, and more.|
|[YAML](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)|YAML Language Support by Red Hat, with built-in Kubernetes syntax support|

## Tools
| Name      | Description      | Notes |
| --- | --- | --- |
| [7-Zip](https://www.7-zip.org/download.html) | 7-Zip is free software with open source. It allows you to compress and extract more formats than Windows supports. ||
 [AdBlock Plus](https://adblockplus.org/) |Experience a cleaner, faster web and block annoying ads||
| [Microsoft PowerToys](https://docs.microsoft.com/en-us/windows/powertoys/install)||
| [WinXCorners](https://github.com/vhanla/winxcorners)||

## Apps
| Name      | Description      | Notes
| --- | --- | --- |
| [eM Client](https://emclient.com/) |eM Client is a Windows and macOS based email client for sending and receiving emails, managing calendars, tasks, contacts, and notes. | Install if you want a responsive email client with a unified inbox.
| [The Matrix Screensaver](https://www.meticulous-software.co.uk/TheMatrix115.zip) |This is the latest version of the Matrix Screensaver emulating the introduction to the movie and the code. Created because of the official screensaver is completely awful. Ten years old and still the best... in fact, now even better!|The Windows 11 screensavers are old and scarce (screensavers are a dying breed). *Install this one if you want a screensaver that looks like it came from the first Matrix movie.*|

* 3D Mark
* 7-Zip
* Bitwarden
* Discord
* Chrome
* RealVnc VNC Viewer
* Team Viewer
* SysInternals Suite

### Edge Extensions
* [Adblock Plus](https://microsoftedge.microsoft.com/addons/detail/adblock-plus-free-ad-bl/gmgoamodcdcjnbaobigkjelfplakmdhh)
* [Bitwarden](https://microsoftedge.microsoft.com/addons/detail/bitwarden-free-password/jbkfoedolllekgbhcbcoahefnbanhhlh)
* [Honey](https://microsoftedge.microsoft.com/addons/detail/honey/amnbcmdbanbkjhnfoeceemmmdiepnbpp)
* [Picture-in-Picture](https://chrome.google.com/webstore/detail/picture-in-picture-extens/hkgfoiooedgoejojocmhlaklaeopbecg)
* [iCloud Bookmarks](https://chrome.google.com/webstore/detail/icloud-bookmarks/fkepacicchenbjecpbpbclokcabebhah)
* [iCloud Passwords](https://microsoftedge.microsoft.com/addons/detail/icloud-passwords/mfbcdcnpokpoajjciilocoachedjkima)

### MS Store
* Modern Flyouts
* HEVC Video Extensions
* Remote Desktop

## Gaming
* [Steam](https://cdn.akamai.steamstatic.com/client/installer/SteamSetup.exe)
* [Battlenet](https://www.blizzard.com/download/confirmation?platform=windows&locale=en_US&product=bnetdesk)
* [Origin](https://www.dm.origin.com/download)
* Oculus


