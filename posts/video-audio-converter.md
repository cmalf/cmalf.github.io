---
title: Video Audio Converter
date: 2024-10-17 14:18:50 +07:00
description: Simple Script NodeJs To Convert Audio or Video with `ffmpeg`
image : /assets/img/Post/VideoConverters.jpeg
author: "cmalf"
---

# Audio-Video-Converter
Simple Script NodeJs To Converts Audio or Video witH `ffmpeg`

## `Source` CODE

```javascript

const { execSync, spawn } = require('child_process');
const readline = require('readline');

const supportedFormats = {
    "Video Formats": ["MP4", "AVI", "MKV", "MOV", "WMV", "FLV", "3GP", "WEBM", "MPEG", "VOB", "DAT", "TS"],
    "Audio Formats": ["MP3", "WAV", "AAC", "OGG", "FLAC", "AC3", "WMA"],
};

function printSupportedFormats() {
    console.log("Supported Formats:");
    for (const [category, formats] of Object.entries(supportedFormats)) {
        console.log(`\x1b[1;32m${category}:\x1b[0m`);
        formats.forEach(format => {
            console.log(`\x1b[1;33m- ${format}\x1b[0m`);
        });
    }
}

function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function pulsingDots() {
    let dots = "";
    for (let i = 0; i < 5; i++) {
        process.stdout.write(`\r\x1b[1;33mStill Processing ${dots}\x1b[0m`);
        dots += ".";
        await sleep(500);
    }
}

async function loadingBar() {
    const chars = ['🔴','🔵','🟡','🟢'];
    for (let i = 0; i < 20; i++) {
        process.stdout.write(`\r\x1b[1;37m[${'🟩'.repeat(i)}${chars[i % 4]}]\x1b[0m`);
        await sleep(500);
    }
    console.log();
}

async function spinningWheel() {
    const chars = ['|', '/', '-', '\\'];
    for (let i = 0; i < 10; i++) {
        process.stdout.write(`\r\x1b[1;37mConverting ${chars[i % 4]}\x1b[0m`);
        await sleep(200);
    }
}

async function convertMedia(inputPath, outputPath) {
    const startTime = Date.now();
    const command = `ffmpeg -i ${inputPath} ${outputPath}`;
    
    const ffmpeg = spawn('ffmpeg', ['-i', inputPath, outputPath], { stdio: 'ignore' });

    while (ffmpeg.exitCode === null) {
        await pulsingDots();
        await loadingBar();
        await spinningWheel();
    }
    
    const endTime = Date.now();
    const duration = (endTime - startTime) / 1000;
    console.log(`\n\x1b[1;32mConversion completed in ${duration.toFixed(2)} seconds. on \x1b[0m${inputPath}`);
}

async function main() {
    printSupportedFormats();
    
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    const inputPath = await new Promise(resolve => {
        rl.question('\n\x1b[1;34mEnter the path of the video or audio file to convert: \x1b[0m', resolve);
    });

    const outputFormat = await new Promise(resolve => {
        rl.question('\x1b[1;34mEnter the desired output format (with extension): \x1b[0m', resolve);
    });

    rl.close();

    const outputPath = `${inputPath.split('.').slice(0, -1).join('.')}.${outputFormat}`;
    console.clear();
    console.log(`

╭━━━╮╱╱╱╱╱╱╱╱╱╱╱╱╱╭━━━┳╮
┃╭━━╯╱╱╱╱╱╱╱╱╱╱╱╱╱┃╭━━┫┃
┃╰━━┳╮╭┳━┳━━┳━━┳━╮┃╰━━┫┃╭╮╱╭┳━╮╭━╮
┃╭━━┫┃┃┃╭┫╭╮┃╭╮┃╭╮┫╭━━┫┃┃┃╱┃┃╭╮┫╭╮╮
┃┃╱╱┃╰╯┃┃┃╰╯┃╰╯┃┃┃┃┃╱╱┃╰┫╰━╯┃┃┃┃┃┃┃
╰╯╱╱╰━━┻╯╰━╮┣━━┻╯╰┻╯╱╱╰━┻━╮╭┻╯╰┻╯╰╯
╱╱╱╱╱╱╱╱╱╱╱┃┃╱╱╱╱╱╱╱╱╱╱╱╭━╯┃
╱╱╱╱╱╱╱╱╱╱╱╰╯╱╱╱╱╱╱╱╱╱╱╱╰━━╯
    `);
    console.log('\x1b[1;33mStarting conversion...\x1b[0m');
    await convertMedia(inputPath, outputPath);
}

main();

```

## About

This script can converts Audio/Video Format to another Format,

- supportedFormats
  
```javascript
const supportedFormats = {
    "Video Formats": ["MP4", "AVI", "MKV", "MOV", "WMV", "FLV", "3GP", "WEBM", "MPEG", "VOB", "DAT", "TS"],
    "Audio Formats": ["MP3", "WAV", "AAC", "OGG", "FLAC", "AC3", "WMA"],
};
```
### Example
- VIDEO
  - MP4 To AVI
  - MP4 To WEBM
  - etc.
- AUDIO
  - MP3 To AAC
  - etc
- Video To Audio
  - MP4 To MP3
  - etc.

## HOW TO USE

### Install `ffmpeg` First
* MacOS with Brew
  ```bash
  brew install ffmpeg
  ```
* Installing FFmpeg on Linux
  
1\. **Update Package Lists:**

-   Ensure your package lists are up-to-date:

    Bash

    ```
    sudo apt update  # For Debian-based distros (Ubuntu, Mint, etc.)
    sudo dnf update  # For Fedora-based distros
    sudo pacman -Syu  # For Arch-based distros

    ```

 2\. **Install FFmpeg:**

-   Use your distribution's package manager to install FFmpeg:

    Bash

    ```
    sudo apt install ffmpeg  # For Debian-based distros
    sudo dnf install ffmpeg  # For Fedora-based distros
    sudo pacman -S ffmpeg  # For Arch-based distros

    ```
 3\. **Verify Installation:**

-   Check the FFmpeg version:

    Bash

    ```
    ffmpeg -version

    ```
-   If installed correctly, you'll see the FFmpeg version information.

 ### Download the Script with git

 ```bash
 git clone https://github.com/caturmahdialfurqon/Audio-Video-Converter.git
 ```
  * Install Requirements/Dependensis NodeJs
```bash
npm install readline child_process
```
 * Run the Script

 ![Video Audio Converter](assets/img/Post/Video-Auido-Converter/CleanShot 2024-10-16 at 09.03.21.gif)

