# Catalina-GPU-Buyers-Guide

**Disclaimer: I mention Turing, Pascal and Maxwell to help educate users on what versions of macOS they're supported on but if you accidentally fell on this page thinking your RTX card is supported, please read carefully**

* [A quick refresher with Nvidia and WebDrivers](README.md#a-quick-refresher-with-Nvidia-and-WebDrivers)
* [So if my GPU is natively supported, why do i need Lilu and WhateverGreen?](README.md#so-if-my-GPU-is-natively-supported-why-do-i-need-Lilu-and-WhateverGreen)
* [So what are my options?](README.md#so-what-are-my-options)
* [Can I run an unsupported GPU in my hack?](README.md#can-I-run-an-unsupported-GPU-in-my-hack)
* [Native AMD GPUs](README.md#Native-AMD-GPUs)
   * Vega 20 series
   * Vega 10 series
   * Radeon 400/500 series (Polaris)
   * GCN 3 and older based Cards
* [Unsupported AMD GPUs](README.md#Unsupported-AMD-GPUs)
   * Navi 10 Series
   * Lexa Series
   * AMD APUs
* [Native nVidia GPUs](README.md#Native-nVidia-GPUs)
   * Kepler Series
* [Unsupported nVidia GPUs](README.md#Unsupported-nVidia-GPUs)
   * Turing Series
   * Pascal Series
   * Maxwell Series
* [Intel’s Integrated Graphics](README.md#Intels-Integrated-Graphics)
   * Westmere i3/5/7-xxx
   * Sandy Bridge i3/5/7-2XXX
   * Ivy Bridge i3/5/7-3XXX
   * Haswell i3/5/7-4XXX
   * Broadwell i3/5/7-5XXX
   * Skylake i3/5/7-6XXX
   * Kabylake i3/5/7-7XXX
   * Kabylake refresh/ Coffeelake i3/5/7-8XXX/9XXX
* [GPUs for different Use Cases](README.md#GPUs-for-different-Use-Cases)
   * GPUs To Avoid
   * Fanless GPUs(0 DB)
   * Single Slot GPUs
   * Half-height GPUs
   * The most powerful GPUs
   * Cheapest Hackintosh GPUs
   * Overall best Hackintosh GPUs
* [Hey I'm lazy, just tell me what to buy](README.md#Hey-Im-lazy-just-tell-me-what-to-buy)

So it's that time of year again, a new version of macOS has been released and the age-old question will be asked once again:

**What GPUs are supported with macOS 10.15 Catalina?**

Well you've come to the right place, I'll give a quick rundown on the situation and go into more detail on exact GPUs we recommend. While this is named the Catalina GPU Buyers guide, this has info for High Sierra, Mojave and Catalina. And for those interested, you can find my old Mojave GPU Buyer's Guide [here](https://www.reddit.com/r/hackintosh/comments/b91vf5/mojave_gpu_buyers_guide/)


# A quick refresher with Nvidia and WebDrivers

![WebDrivers](WebDrivers.gif)

Well currently as of the time of writing, we've gone a full OS cycle without official drivers from Nvidia for their Maxwell, Pascal or Turing GPUs. What this means is that users of these GPUs have no support for either Mojave or Catalina so are stuck with macOS 10.13 High Sierra. Who's to blame? Well it's 2 giant, egotistical companies who both refuse to work together so the blame can go both ways. Do keep in mind that the WebDrivers have a VRAM leakage issue that they've yet to address, so a theory to why Apple refuses Nvidia drivers in macOS may be due to how Nvidia refuses to hand over the driver stack. Think it's a coincidence that both AMD and intel have open-sourced drivers? Well, either way, it doesn't change the fact there's no support. 

Users with Kepler based GPUs are in the clear though, they utilize Apple's native drivers

# So if my GPU is natively supported, why do i need Lilu and WhateverGreen?

This is a question comes up quite a bit in the Hackintosh community, and for good reason as to why in the world would these GPUs work out of the box on a mac and not a Hackintosh? Well, the reason being is that PCs and Macs have different internal wiring and so the ACPI layouts in a PC don't work well with Macs in different scenarios. To get around this, we use [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases) and it's companion [Lilu](https://github.com/acidanthera/Lilu/releases) to patch different parts of our Hackintosh like renaming devices, assisting in framebuffer connections, patching audio connectors, allowing modifications to aty_config, aty_properties, cail_properties via ACPI and so much more. With such a large feature set and developed by someone who knows what they're doing, there's no reason not to use it

# So what are my options?


So there’s still 2 routes for discrete GPUs you can go, either AMD or Nvidia(Yes, there’s actually natively supported Nvidia cards in Catalina). So I’ll be going over what GPUs are compatible and what features/drawbacks they hold.

Things to remember:

* macOS does not support either SLI, Crossfire or GPUs will multiple main cores(like the Radeon Pro Duo). This may change with the release of the Radeon Pro Vega II Duo in the Mac Pro
* Getting audio through HDMI/DisplayPort may require extra work with both AppleALC.kext and some other IO-REG edits
* GPU Overclocking is limited to Vega 10 GPUs with [PyVega](https://github.com/corpnewt/PyVega)
* Running a supported GPU with an unsupported GPU can have weird consequences as unsupported GPUs run off VESA drivers which have the issue in which it can break sleep and other functions in macOS. Please refer to the [Disabling unsupported GPUs Guide](https://github.com/khronokernel/How-to-disable-your-unsupported-GPU-for-MacOS) for more info

# Can I run an unsupported GPU in my hack?

So something to keep in mind when running an unsupported GPU in macOS is will fall back on VESA drivers when no real drivers are present. These are very simple, CPU based drivers that are used as a stop-gap while you wait to install the correct drivers but many baisc functions of macOS are broken when running this way including sleep and general stability. And since these GPUs have no drivers even outside of Apple, we need some way to stop the unsupported GPU from being recognized in macOS. So what do we do? Well I'm glad you ask. With my patent pending [How to disable your unsupported GPU for macOS Guide](https://github.com/khronokernel/How-to-disable-your-unsupported-GPU-for-MacOS/blob/master/README.md), even a simpleton like you can experience the glories of Mojave and beyond!

`But can render macOS on my iGPU but use the video outs on my unsupported GPU?`

Unfortunately not, and the reason being is actually quite similar to how Nvidia's Optimus technology functions. You would first need a way to grab/encode the iGPU's signal, send it towards the discrete GPU, then have said GPU decode the signal and display it. One small problem, decoding the signal would require proper GPU acceleration which your unsupported GPU doesn't have. So you will need to use your motherboard's video out ports no matter what

# Native AMD GPUs

**Vega 20 series Highest Supported OS: Current/Catalina**

So all Vega based GPUs are natively supported in macOS with Vega 20 GPUs starting in Mojave. While natively supported, it's recommended to still have WhateverGreen.kext installed as this helps with proper framebuffer connections and fixes other odd issues like proper ACPI mapping and such

Supported Cards:

* Radeon VII

Needed kexts:

* [lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)


**Vega 10 series Highest Supported OS: Current/Catalina**

Just like with Vega 20, Vega 10 GPUs are natively supported in macOS though these card's support starts in High Sierra. Similar to Vega 20, it's recommended to still have WhateverGreen.kext installed as this helps with proper framebuffer connections and fixes other odd issues like proper ACPI mapping and such.

And for those who want to overclock/undervolt, check out [PyVega](https://github.com/corpnewt/PyVega)

The only brand of GPUs to **avoid with Vega 10 are XFX and Sapphire**. The reason being is VBIOS communication issues which can't be easily solved with a reference BIOS due to how Vega's powerplay table interacts between the OS and GPU.

Supported Cards:

* Vega 64 Liquid
* Vega 64
* Vega 56

Radeon Pro:
* Vega Frontier Edition
* Radeon Pro WX 9100
* Radeon Pro WX 7100

Needed kexts:

* [lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)

**Radeon 400/500 series (Polaris) Highest Supported OS: Current/Catalina**

Regarding Polaris, basically every model of card is supported as long as it’s running a Polaris core(lower end cards like the RX550 run a Lexa core meaning no support in macOS).

The only brand of GPU **you should** **avoid with the Polaris series would be XFX and ASRock** as many users have had issues with these cards with viewing Clover and macOS booting but other users have found fixes/workarounds(though nothing consistent). This seems to be caused by having an odd VBIOS that doesn't communicate well with macOS and the only real solution is flashing another VBIOS which is not ideal for most users.

Supported cards:

400 Series:

* RX 480
* RX 470D
* RX 470
* RX 460

500 Series:
* RX 590
* RX 580X
* RX 580
* RX 570X
* RX 570
* RX 560X
* RX 560

Radeon Pro:

* WX 5100
* WX 4100
* WX 3100
* WX 2100


Needed kexts:

* [lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)


**GCN 3 and older based Cards**

Regarding GCN 3 and older, cards from these generations theoretically will have support for Metal in Catalina but due to how fragmented some of the product stack became meant that some cards may not have support. Generally, HD 7XXX series of GPUs and up are metal compatible but I’ll only list GPUs that have been proven to work.

**Radeon R9 3xx (Fiji) Current/Catalina**

Fiji is also natively supported in Catalina without much issue but we cannot guarantee the success of R5 and R7 cards due to not having many reports of success soon them. Also, be wary that differing from the reference design of these cards have many more issues that require a lot of work to get them to run properly

Supported cards:

* R9 Fury X
* R9 Fury
* R9 Nano
* R9 390(FakeID needed)
* R9 290X/390X
* R9 290/390(FakeID needed)
* R9 280x/380x
* R9 280/380
* R9 270X/370X
* R7 270/370
* R7 265
* R7 260x/360x
* R9 260/360
* R7 250
* R7 240

Needed kexts

* [lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)

# Unsupported AMD GPUs

**Navi 10 Series (RX 5000) Highest Supported OS: None**

Currently, as of writing, Apple has not released any Navi based drivers for macOS. Because of this, you'll need to block out the GPU if you want to use another GPU as VESA drivers that unsupported GPUs runs off of break sleep and other functions in macOS. Please refer to the [Disabling unsupported GPUs Guide](https://www.reddit.com/r/hackintosh/comments/bu1wf8/how_to_disable_your_unsupported_gpu_for_macos/)

Unsupported Cards:

* RX 5700
* RX 5700 XT
* RX 5700 XT 50th Anniversary Edition

**Lexa Series (RX 500) Highest Supported OS: None**

While these GPUs may share the same family name as the Polaris GPUs, these cards are drastically different meaning no support in any version of macOS. Similar to Navi and unsupported Nvidia GPUs, you'll need to disable the Lexa GPU due to how the Vesa drivers that unsupported GPUs run off of break sleep and other functions in macOS. Please refer to the [Disabling unsupported GPUs Guide](https://www.reddit.com/r/hackintosh/comments/bu1wf8/how_to_disable_your_unsupported_gpu_for_macos/)

Unsupported Cards:

* RX 550X
* RX 550
* RX 540X
* RX 540

**AMD APUs (ALL VARIENTS) Highest Supported OS: None**

The integrated GPU found on lower end AMD CPUs have unfortunatly never had offical support with community support quite lacking. While possible to get a display out with some work, graphics acceleration is basically imposiible making these APUs more of a hazard to macOS

Unsupported APUs:
* Vega 11(Zen)
* Vega 8(Zen)
* GCN 3(Escavator Gen 2, Steamroller) 
* GCN 2(Escavator Gen 1, Puma, Puma +)


# Native nVidia GPUs

**Kepler Series (GTX 6xx, 7xx) Highest Supported OS: Current/Catalina**

Currently the only 100% native Nvidia architecture that works with Catalina. Users have reported issues with the GTX 650Ti, 660, 660ti but this is caused by a driver issue on Apple’s end by not supporting the GK106 core(or quite poorly as the issue seems to be memory leakage which also affects real Macs). Another issue with this generation is lower end products marketed as first generation Kepler are actually using a Fermi core but have identical counterparts running Kepler cores as well(GF 116 vs GK 107 found in the GT 640). **AND PLEASE NOTICE THAT  GTX 745, 750 and ti VARIANTS ARE NOT INCLUDED, THEY'RE NOT KEPLER**

Supported cards:

Kepler Gen 2:

* GTX Titan (GK 110 Maxwell core)
* GTX Titan Black(GK 110 Maxwell core)
* GTX Titan Z (One of the few dual GPU cards supported in MacOs)
* GTX 780 Ti
* GTX 780
* GTX 770
* GTX 760 Ti
* GTX 760
* GT 740
* GT 730(GK208 variant)
* GT 720
* GT 710

Kepler Gen 1:

* GTX Titan (GK 110 Maxwell core)
* GTX Titan Black(GK 110 Maxwell core)
* GTX Titan Z (One of the few dual GPU cards supported in MacOs, unfortunately was never truly utilized)
* GTX 690(Another dual GPU card compatible with macOS)
* GTX 680
* GTX 670
* GTX 660 Ti
* GTX 660(MUST BE RUNNING A GK 104 core, NOT GK 106)
* GTX 650(GK 107 core)
* GT 640(Kepler edition, GK 107/208 core)
* GT 630(Kepler edition, GK 107/208 core)

Quadro:

* Quadro K6000
* Quadro K5200
* Quadro K5000
* Quadro K4200
* Quadro K2000D
* Quadro K2000
* Quadro K600
* Quadro K420
* Quadro 410

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)


# Unsupported nVidia GPUs

**Turing Series (RTX 20xx, GTX 16xx) Highest Supported OS:NONE**

Unfortunately, no support in any version of macOS as no drivers were ever written even for High Sierra. Not much else to add.

These cards include:

* Titan RTX
* RTX 2080 Ti
* RTX 2080 Super
* RTX 2080
* RTX 2070 Super
* RTX 2070
* RTX 2060 Super
* RTX 2060
* GTX 1660 Ti
* GTX 1660
* GTX 1650

Quadro:

* Quadro RTX 8000
* Quadro RTX 6000
* Quadro RTX 5000
* Quadro RTX 4000


**Volta Series Highest Supported OS:NONE**

The same idea as Turing, no drivers were ever written

These cards include:

* Titan V
* Titan V CEO Edition

Quadro:

* Quadro GV100

**Kepler Series(GK 106 Variants)**

GPUs running the GK 106 core have the unfortunate concequene of having a serious issue regarding VRAM leakage. This means that there's a high chance of disotrion and overall instabilty when running these GPUs which unfortuanty have no real solution as even installing web drivers has no affect. A list of GPUs with this core can be found [here](https://www.techpowerup.com/gpu-specs/nvidia-gk106.g186)

Second generation Kepler:

* GT 740

First generation Kepler:

* GTX 660
* GTX 650 Ti
* GTX 650
* GTX 645

Quadro:

* K4000

**Pascal Series (GTX 10xx) Highest Supported OS: High Sierra 10.13.6**

Well pretty sure most users know what going on with Pascal and Maxwell but I’ll just mention it quickly here. No support for these cards in Mojave/Catalina but macOS High Sierra 10.13.6 do support these cards with the combination of Nvidia’s somewhat shotty drivers and Lilu+WhateverGreen

Supported cards:

* GTX Titan X(GP 102-400 Pascal core)
* GTX Titan Xp(GP 102-450 Pascal core)
* GTX 1080 Ti
* GTX 1080
* GTX 1070 Ti
* GTX 1070
* GTX 1060
* GTX 1050 Ti
* GTX 1050
* GT 1030

Quadro:

* Quadro GP100
* Quadro P6000
* Quadro P5000
* Quadro P4000
* Quadro P2000
* Quadro P1000
* Quadro P620
* Quadro P600
* Quadro P400

Needed kexts:

* [Nvidia’s Web drivers](https://www.nvidia.com/download/driverResults.aspx/125379/en-us)
* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)


**Maxwell Series (GTX 9xx, 745, 750 and ti variant) Highest Supported OS: High Sierra 10.13.6**

Same idea as Pascal, though the naming scheme is a bit odd as the GTX 745, 750 and 750ti are all Maxwell based even though they’re being marketed with the Kepler line so be wary when buying

Supported cards:

* GTX Titan X(GM 200 Maxwell core)
* GTX 980 Ti
* GTX 980
* GTX 970
* GTX 960
* GTX 950
* GTX 750 Ti
* GTX 750
* GTX 745

Quadro:

* Quadro M6000
* Quadro M5000
* Quadro M4000
* Quadro M2000
* Quadro K220
* Quadro K1200
* Quadro K620
* NVS 510

Needed kexts:

* [Nvidia’s Web drivers](https://www.nvidia.com/download/driverResults.aspx/125379/en-us)
* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)

# Intel's Integrated Graphics

So I'll be going over the compatible iGPUs present in intel's CPUs, the main thing to note is that you'll need to apply the FrameBuffer patch to your system to get things to work properly. [Please refer to this post for more info on Framebuffer patching as it goes in depth on how to get your system running](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271). We will also be excluding iGPUs present in Pentiums, Celerons and Atom CPUs as these generally have never been supported natively and require quite a bit of extra work to get them working


**Westmere i3/5/7-xxx Highest Supported OS: High Sierra 10.13.6**

Unfortunately, Mojave dropped support for these iGPUs but luckily we can actually get these iGPUs working by using old kexts(though no Metal support so things are a bit iffy). I won't link any of the files myself so do be wary when downloading kexts off the internet

* HD Graphics (yup, that's all they called them)

Files needed:

* GPUSupport.framework
* OpenGL.framework

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)

**Sandy Bridge i3/5/7-2XXX Highest Supported OS: High Sierra 10.13.6(With a bit of work, current/Catalina)**

Unfortunately, Mojave dropped support for these iGPUs but luckily we can actually get these iGPUs working by using old kexts(though no Metal support so things are a bit iffy). I won't link any of the files myself so do be wary when downloading kexts off the internet. Intial supported introduced with macOS 10.7 and is not supported by the [Intel framebuffer patch](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)

Supported iGPUs:

* HD 2000
* HD 3000

Framebuffer
* AAPL,snb-platform-id (desktop): 0x00030010 (default)
* AAPL,snb-platform-id (laptop): 0x00010000 (default)

Files needed for HD 2000:

* AppleIntelHDGraphicsFB.kext
* AppleIntelHDGraphicsGA.plugin
* AppleIntelHDGraphicsGLDriver.bundle
* AppleIntelHDGraphicsVADriver.bundle

Files needed for HD 3000:

* AppleIntelHD3000Graphics.kext
* AppleIntelHD3000GraphicsGA.plugin
* AppleIntelHD3000GraphicsGLDriver.bundle
* AppleIntelHD3000GraphicsVADriver.bundle
* AppleIntelSNBGraphicsFB.kext
* AppleIntelSNBVA.bundle

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)


**Ivy Bridge i3/5/7-3XXX Highest Supported OS: Current/Catalina**

Regarding the HD 4000, it's completely native with Catalina. The HD 2500 on the other hand only has partial support in Mojave for quick sync features as hardware acceleration is [unsupported](https://olarila.com/forum/viewtopic.php?t=7714) so you will need a compataible GPU for display purposes. Intial supported introduced with macOS 10.8

Supported iGPUs:

* HD 2500
* HD 4000

Framebuffer:

* AAPL,ig-platform-id (desktop):
   * 0x0166000A (default)
   * 0x01620005
* AAPL,ig-platform-id (laptop): 
   * 0x01660003 (default)
   * 0x01660009
   * 0x01660004

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)


**Haswell i3/5/7-4XXX Highest Supported OS: Current/Catalina**

Most iGPUs are supported here, only one to be concerned about is the HD4400 which requires either a spoofed DeviceID with WhateverGreen or a modfied APCI path. Intial supported introduced with macOS 10.9

Supported iGPUs:

* HD 4200
* HD 4400(FakeID required for this iGPU)
* HD 4600
* HD 5000
* HD 5100
* HD P4600(Theoretically)
* HD P4700(Theoretically)

Framebuffer:

* AAPL,ig-platform-id (desktop): 
   * 0x0D220003 (default)
* AAPL,ig-platform-id (laptop): 
   * 0x0A160000 (default)
   * 0x0A260005 (recommended)

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)


**Broadwell i3/5/7-5XXX Highest Supported OS: Current/Catalina**

All iGPUs are supported here, no issues to report. Intial supported introduced with macOS 10.10.2

Supported iGPUs:

* HD 5300
* HD 5500
* HD 5600
* HD 6000
* HD 6100
* HD 6200
* HD P5700(Theoretically)
* Iris Pro P6300

Framebuffer:

* AAPL,ig-platform-id (desktop): 
   * 0x16220007 (default)
* AAPL,ig-platform-id (laptop): 
   * 0x16260006 (default)

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)


**Skylake i3/5/7-6XXX Highest Supported OS: Current/Catalina**

All iGPUs are supported here, no issues to report. Intial supported introduced with macOS 10.11.4

Supported iGPUs:

* HD 510
* HD 515
* HD 520
* HD 530
* HD P530
* Iris 540
* Iris 550
* Iris Pro 580
* Iris Pro P555
* Iris Pro P580

Framebuffer:
* AAPL,ig-platform-id (desktop): 
   * 0x19120000 (default)
* AAPL,ig-platform-id (laptop): 
   * 0x19160000 (default)

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)


**Kabylake i3/5/7-7XXX Highest Supported OS: Current/Catalina**

Most iGPUs are supported here excluding the HD 610 present in the Pentium G4560, initial support was introduced with macOS 10.12.6

Supported iGPUs:

* HD 615
* HD 620
* HD 630
* Iris Plus 640
* Iris Plus 650

Framebuffer:
* AAPL,ig-platform-id (desktop): 
   * 0x59160000 (default)
* AAPL,ig-platform-id (laptop): 
   * 0x591B0000 (default)

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)


**Kabylake refresh/ Coffeelake i3/5/7-8XXX/9XXX Highest Supported OS: Current/Catalina**

All iGPUs are supported here, though pay attention as the [i3 8100 and 8350k use a different UHD 630(184 shader units vs 192)](https://en.wikipedia.org/wiki/Intel_Graphics_Technology#Kaby_Lake_Refresh_/_Amber_Lake_/_Coffee_Lake_/_Whiskey_Lake) than the rest of the CPU family which requires spoofing for support in High Sierra(generally wanted for headless rendering on a Maxwell/Pascal GPUs). Intial supported introduced with macOS 10.13.6

* UHD 610
* UHD 620
* UHD 630
* Iris Plus 655

Framebuffer:
* AAPL,ig-platform-id (desktop): 
   * 0x3EA50000 (default) 
   * 0x3E9B0007 (recommended)
* AAPL,ig-platform-id (laptop): 
   * 0x3EA50009 (default)

Needed kexts:

* [Lilu.kext](https://github.com/acidanthera/Lilu/releases)
* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen/releases)
* [Intel FrameBuffer Patching guide](https://www.insanelymac.com/forum/topic/334899-intel-framebuffer-patching-using-whatevergreen/?tab=comments#comment-2626271)
# GPUs for different Use Cases

So you just want a GPU recommendation? Well honestly in the current situation the only cards we'd recommend would be from AMD that are either Polaris(Rx 4xx, 5xx) or newer as GCN 3 and older can loose support at any time and the same applies for Nvidia's Kepler. Here are the cards we recommend and do remember that reference cards are generally the safest solution

**GPUs To Avoid**

With GPUs to avoid it's a bit of a mixed bag, the speific brands to avoid 100% are Powercolor and XFX regardless of what core they run. They're the most common GPUs to have instabiltiy issues and many users will outright not get any video out past the Clover bootscreen making a macOS install virtually impossible. And while Sapphire may be the best brand for Polaris GPUs, Vega GPUs are quite a bit of a different story. While many have working systems with Sapphire Vega, a good chunk of users also experience instability and issues with macOS functioning correctly. 

And for those who are wondering why this list contradicts [Tonymacx86's buyers guide](https://www.tonymacx86.com/buyersguide/building-a-customac-hackintosh-the-ultimate-buyers-guide/#AMD_Graphics_Cards), remember that their bottom line is to get users to  buy hardware through their affiliate program. This is also the same website that recommended Pascal GPUs [5 months after Mojave's release](https://web.archive.org/web/20190213211919/https://www.tonymacx86.com/buyersguide/building-a-customac-hackintosh-the-ultimate-buyers-guide/), would you really trust a website that's neither kept up-to date and offers *shivers* the [beast tools](https://github.com/khronokernel/Tonymcx86-stance)?

Powercolor(**ALL MODELS**)

* [PowerColor Red Devil RX VEGA 56/64](https://www.powercolor.com/product?id=1511340918)
* [PowerColor Red Dragon/Devil RX 580](https://www.powercolor.com/products?id=1492658578&type=1493173705)
* [PowerColor Red Dragon RX 560/570](https://www.powercolor.com/products?id=1492658578&type=1493173679)

XFX(**ALL MODELS**)

* [XFX Reference RX Vega 56/64](http://xfxforce.com/en-us/products/amd-radeon-vega#*)
* [XFX Vega 56 Double Dissipation](http://xfxforce.com/en-us/products/amd-radeon-vega/amd-radeon-rx-vega-56-hbm2-8gb-3xdp-hdmi-double-dissipation-rx-vegaldff6)
* [XFX RX 590 Fatboy](http://xfxforce.com/en-us/products/amd-radeon-rx-500-series#*)
* [XFX RX 580/570/560](http://xfxforce.com/en-us/products/amd-radeon-rx-500-series#*)

Sapphire(**ONLY VEGA MODELS**)

* [Sapphire Reference Vega 56/64](https://www.sapphiretech.com/en/consumer/21275-02-radeon-rx-vega64-8g-hbm2)
* [Sapphire NITRO+ RX VEGA 56/64](https://www.sapphiretech.com/en/consumer/nitro-rx-vega64-8g-hbm2)
* [Sapphire Pulse Vega 56](https://www.sapphiretech.com/en/consumer/pulse-rx-vega56-8g-hbm2)

**Fanless GPUs(0 DB)**

Unfortunalty the variety for fanless GPUs are quite small, while there are many GPUs with fan-stop these aren't perfect solutions. Models with no fan at all are limited to either GT 1030s which are unsupported past High Sierra or the GT 710 which could loose support some time soon

Fanless models:
* [GT 710](https://www.geforce.com/hardware/desktop-gpus/geforce-gt-710/specifications)(basically every model is single slot, half height and many are fanless)

Fan-Stop models(no fan spin under 50/60C generally):

Vega
* [Asus Strix Vega 56/64](https://www.asus.com/ca-en/Graphics-Cards/ROG-STRIX-RXVEGA64-O8G-GAMING/)
* [Gigabyte RX Vega 56/64 Gaming](https://www.gigabyte.com/Graphics-Card/GV-RXVEGA64GAMING-OC-8GD#kf)

Polaris
* [Asus Strix RX 580](https://www.asus.com/ca-en/Graphics-Cards/ROG-STRIX-RX580-O8G-GAMING/)
* [ASUS Dual series RX 580](https://www.asus.com/ca-en/Graphics-Cards/DUAL-RX580-O4G/)
* [Sapphire Pulse RX 580](https://www.sapphiretech.com/en/consumer/pulse-rx-580-8g-g5)
* [Sapphire Nitro RX 580](https://www.sapphiretech.com/en/consumer/nitro-rx-580-8g-g5)
* [Gigabyte RX 580 Gaming](https://www.gigabyte.com/Graphics-Card/GV-RX580GAMING-8GD-rev-10-11-12#kf)

**Single Slot GPUs**

Polaris

* [Sapphire Pulse RX 550 640SP](https://www.sapphiretech.com/en/consumer/pulse-rx-550-2g-g5-1)(make sure it's Polaris based, this is one of the first RX 550 models that run a "true" polaris chip)

Radeon pro Vega

* [Radeon Pro WX 7100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-7100)

Radeon Pro Polaris

* [Radeon Pro WX 5100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-5100)
* [Radeon Pro WX 4100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-4100)
* [Radeon Pro WX 3100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-3100)
* [Radeon Pro WX 2100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-2100)

Nvidia

* [GT 710](https://www.geforce.com/hardware/desktop-gpus/geforce-gt-710/specifications)(basically every model is single slot, half height and many are fanless)

Quadro

* [Quadro K4200](https://www.nvidia.com/content/dam/en-zz/Solutions/design-visualization/quadro-product-literature/DS-NV-Quadro-K4200-JUL24-US-NV-r-HR.pdf)
* [Quadro K2000D](https://www.nvidia.com/content/PDF/data-sheet/DS_NV_Quadro_K2000D_OCT13_NV_US_LR.pdf)
* [Quadro K2000](https://www.nvidia.com/content/PDF/data-sheet/DS_NV_Quadro_K2000_OCT13_NV_US_LR.pdf)
* [Quadro K600](https://www.nvidia.com/content/dam/en-zz/Solutions/design-visualization/quadro-product-literature/DS_NV_Quadro_K600_OCT13_NV_US_lr.pdf)
* [Quadro K420](http://www3.pny.com/file%20library/support/pny%20products/resource%20center/nvidia%20-%20quadro%20graphics%20cards/english/product-brochure/ds_nv_quadro_k420_2gb_sep_2015_us_pny.pdf)
* [Quadro 410](https://www.nvidia.com/content/PDF/data-sheet/nv-quadro-410-lr.pdf)

**Half-height GPUs**

Radeon Pro Polaris

* [Radeon Pro WX 4100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-4100)
* [Radeon Pro WX 3100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-3100)
* [Radeon Pro WX 2100](https://www.amd.com/en/products/professional-graphics/radeon-pro-wx-2100)

Nvidia 

* [GT 710](https://www.geforce.com/hardware/desktop-gpus/geforce-gt-710/specifications)(basically every model is single slot, half height and many are fanless)

Quadro

* [Quadro K600](https://www.nvidia.com/content/dam/en-zz/Solutions/design-visualization/quadro-product-literature/DS_NV_Quadro_K600_OCT13_NV_US_lr.pdf)
* [Quadro K420](http://www3.pny.com/file%20library/support/pny%20products/resource%20center/nvidia%20-%20quadro%20graphics%20cards/english/product-brochure/ds_nv_quadro_k420_2gb_sep_2015_us_pny.pdf)
* [Quadro 410](https://www.nvidia.com/content/PDF/data-sheet/nv-quadro-410-lr.pdf)

**The Most Powerful GPUs**

While it may seem obvious that the most powerful GPU would be the Radeon VII, do keep in mind drivers aren't as mature as Vega 10's drivers. For the best reliablity you'll want to either grab a Vega 10 series GPU(RX Vega 64) or wait for the issues with the MacPro 7,1 to be ironed out

* [Radeon VII](https://www.amd.com/en/products/graphics/amd-radeon-vii)
* [Asus Strix Vega 64](https://www.asus.com/ca-en/Graphics-Cards/ROG-STRIX-RXVEGA64-O8G-GAMING/)
* [Gigabyte RX Vega 64 Gaming](https://www.gigabyte.com/Graphics-Card/GV-RXVEGA64GAMING-OC-8GD#kf)
* [MSI Airboost Vega 64](https://www.msi.com/Graphics-card/Radeon-RX-Vega-64-Air-Boost-8G-OC)

**Cheapest Hackintosh GPUs**

* RX 460/560
* Litterally whatever iGPU came with your CPU

**Overall Best Hackintosh GPUs**

Polaris:
* [Sapphire Pulse RX 580](https://www.sapphiretech.com/en/consumer/pulse-rx-580-8g-g5)
* [MSI Armor RX 580](https://www.msi.com/Graphics-card/Radeon-RX-580-ARMOR-8G-OC.html)
* [Asus Strix RX 580](https://www.asus.com/ca-en/Graphics-Cards/ROG-STRIX-RX580-O8G-GAMING/)

Vega:
* [Asus Strix Vega 56/64](https://www.asus.com/ca-en/Graphics-Cards/ROG-STRIX-RXVEGA64-O8G-GAMING/)
* [Gigabyte RX Vega 56/64 Gaming](https://www.gigabyte.com/Graphics-Card/GV-RXVEGA64GAMING-OC-8GD#kf)
* [MSI Airboost Vega 56/64](https://www.msi.com/Graphics-card/Radeon-RX-Vega-64-Air-Boost-8G-OC)
* [Radeon VII](https://www.amd.com/en/products/graphics/amd-radeon-vii)


Hopefully this little guide helps you, if you have anything else you'd like to add feel free to mention and I'll look into it

\- Your local neighbourhood Hackintosh Slav
