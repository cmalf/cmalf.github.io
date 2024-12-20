---
layout: post
title: The Perfect MacMini Hackintosh
date: 2024-06-02 19:13:24 +07:00
categories: [Hackintosh]
tags: [hackintosh]
description: Perfect Hackintosh HP Elitdesk 800 G4 DM 35W, with SMBIOS MACMINI 2018
image: /assets/img/Post/The-Perfect-MacMini-Hackintosh/Think-different.jpeg
alt: "image alt text"
comments: true
---

## MacMini Hackintosh (HackMini) OC 1.0.0

Unlock the Mac Experience on Your HP EliteDesk!

This hackintosh configuration is designed to bring the best of both worlds: the power and reliability of your HP EliteDesk and the intuitive user experience of macOS.

Specifically optimized for `HP EliteDesk 800 G4 and G5 DM 35W/65W` models, this setup can also be adapted to various Series 800 G4, G5, and SFF models with `CoffeeLake` (CFL) and `CoffeeLake Refresh` (CFLR) processors.

Transform your `HP EliteDesk 800 G4/G5 DM 35W/65W` into a `powerful Mac` with this optimized `hackintosh` configuration. Leveraging the `MacMini 2018` SMBIOS, you can enjoy a seamless macOS experience.

## My System Specs of My HP Elitdesk 800 G4 DM 35W

![HP ELITDESK](https://support.hp.com/wcc-assets/document/images/695/c06047206.png){: w="250" h="500"}

### HP Elitdesk 800 G4 DM 35W 

- Intel Core i5-8500T processor
    - 2.1 GHz (up to 3.5 GHz with Intel Turbo Boost technology)
    - 9 MB cache, 6 cores
    - Supports Intel vPro Technology

- Memory
    - DDR4-2666 16GB 
    - 16 GB total system memory (8 GB x 2)
    - Manufacturer:	Samsung

- Storage
    - PCIe NVMe M.2 SSD drives
        - 256 GB, M.2 2280, PCIe NVMe SSD
        - Manufacturer:	Sandisk
    - 2.5 in SATA SSD drives
        - SATA 256 GB, SATA 6.0 Gb/s
        - Manufacturer:	Samsung

- Graphics
    - Intel UHD Graphics 630

- Ports, Adapters and cables
    - (3) HP DisplayPort to DVI-D adapter
    - USB
        - (3) USB 3.1 Gen 1: (1) front; (2) rear
        - (3) USB 3.1 Gen 2: (1) front, (2) rear
        - (3) USB Type-C 3.1 Gen 2, (1) front; (1) rear: optional
- Networking/communications
    - Ethernet (RJ-45) (integrated)
        - Intel I219LM Gigabit Network Connection LOM (standard)
    - Wireless LAN
        - Intel 9560 802.11ac 2x2 Wi-Fi with Bluetooth M.2 Combo Card vPro
- Audio
    - Conexant CX20632 Audio Codec

## My Hacmini with Sonoma 14.5
<hr>
![hackmini](/assets/img/Post/The-Perfect-MacMini-Hackintosh/Screenshot%202024-06-02%20at%2016.52.30.png){: w="250" h="500" .left} <br>
<br>
<span style="color: #FF0000 !important;">System info and About This Hack</span>

For other just check My github Repository [HP-EliteDesk-800-G4-G5-Hackintosh](https://github.com/cmalf/HP-EliteDesk-800-G4-G5-Hackintosh)

<hr>
<br>
<br><br><br><br>
<br>
## What is not working

- DRM (no hackintosh solution for DRM with UHD 630 iGPU)
- Everything else that I have tested is working perfectly

## What is working

- Everything not mentioned above
- Sleep / Wake
- Multiple displays with IGPU graphics acceleration, hot pluggable display ports and DP->DVI adapters
- USB 3.1 ports
- Type C Port
- Audio (internal speaker and headphone jack)
- Ethernet
- Microphone / front-right audio port (tested with CTIA-style 4-connector headset)
- Airport 
- WIFI 
- BlueTooth (with USB-Port Modified As Dongle)
- for wifi in sequoia (15 - 15.1.1) use `itlwm kext + Heliport` (airport not supported yet)

## Bios Settings

You can see the bios setting with pdf.
> Right Click the file pdf below and `Open Link In New Tab`

- [Bios settings.pdf](/assets/img/Post/The-Perfect-MacMini-Hackintosh/HP%20EliteDesk%20800%20G4%20Mini%20BIOS%20Configuration.pdf)


<br>

## Here To Download the OS

 Here You can directly download `File Image Disk for Macos`
 if you dont have any mac system.

  You can download below!
- [MacOS Sequoia (15.1.1) 24B91](https://swcdn.apple.com/content/downloads/21/19/072-30111-A_4V7Y0VVH1Q/ie1hmy1uaj094z769s4zqmdaojp2vk4dkj/InstallAssistant.pkg)
- [MacOS Sonoma (14.5) 23F79](https://swcdn.apple.com/content/downloads/32/06/062-01946-A_0PEP7JHIWA/1pfs4xh22555dj51fkep7w06s4eiezh21p/InstallAssistant.pkg)
- [MacOS Ventura (13.6.7) 22G720](https://swcdn.apple.com/content/downloads/46/31/052-96247-A_MLN9N00Y8W/dmml3up52hrsb01krjtczmdhexiruv1b5m/InstallAssistant.pkg)
- [MacOS Monterey (12.7.5) 21H1222](https://swcdn.apple.com/content/downloads/02/18/052-96238-A_V534Q7DYXO/lj721dkb4wvu0l3ucuhqfjk7i5uwq1s8tz/InstallAssistant.pkg)
- [macOS Big Sur (11.7.10) 20G1427 ](https://swcdn.apple.com/content/downloads/14/38/042-45246-A_NLFOFLCJFZ/jk992zbv98sdzz3rgc7mrccjl3l22ruk1c/InstallAssistant.pkg)

For another version You can visit [Mr. Macintosh](https://mrmacintosh.com/)

> Don't worry the Source link is Officially from Apple. `http://swcdn.apple.com/`
{: .prompt-warning }

## My EFI with OC `Opencore`

- Release EFI OC 1.0.0 on My Repository [here](https://github.com/caturmahdialfurqon/HP-Elitdesk-800-G4-G5-Hackintosh)

- Release EFI OC 1.0.2 on My Release [here](https://github.com/cmalf/HP-EliteDesk-800-G4-G5-Hackintosh/releases/tag/OC1.0.2-EFI-R001)

> This EFI can be Use for both Bootable and System
{: .prompt-tip }

## For Installation

> Dont forget before installing Macos SONOMA and SEQUOIA set First `SecureBoot` to `Disable` For smooth Installation. You can set to `default` after installation.
{: .prompt-tip }

`Update` ❗✎ᝰ. For Now Onwards

> I think it's better to set SBM to `permanent disabled`. both `Sonoma` and `Sequoia`
{: .prompt-tip }