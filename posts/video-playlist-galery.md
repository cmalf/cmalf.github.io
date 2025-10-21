---
title: Video Playlist Gallery
date: 2024-07-08 03:15:44 +07:00
description: Create A Responsive Video Playlist Gallery Using HTML - CSS - Javascript
image : /assets/img/Post/vgm1.gif
author: "cmalf"
---

# Video-Playlist-Gallery

## Create A Responsive Video Playlist Gallery Using HTML - CSS - Javascript

This script written with php can Instantly Create a single `HTML` file including `CSS` and `JAVASCRIPT`.
For Your Video Gallery, also you can watch it Offline on your browser.

## Updated Codes at 2024-09-02

View Release code : [Release-VGM](https://github.com/caturmahdialfurqon/Video-Playlist-Gallery/releases)

## `Source` CODE

```php
<?php
system("clear");

$Exstentions = [
    "Video Exstentions" => ["MP4", "MP3", "AVI", "MKV", "MOV", "WMV", "FLV", "3GP", "WEBM", "MPEG", "VOB", "DAT", "TS"],
];

function printExstentions() {
    global $Exstentions;
    $index = 1;
    foreach ($Exstentions as $category => $formats) {
        echo "\033[1;34m" . $category . ":\033[0m\n";
        foreach ($formats as $format) {
            echo "\033[1;32m $index. " . $format . "\033[0m\n";
            $index++;
        }
    }
}

printExstentions();
$choice = (int)readline("Choose Your Video Extension Format (number) => ");
$Exstention = $Exstentions["Video Exstentions"][$choice - 1] ?? "Invalid choice";
$directory = readline("Enter Directory Path Here => ");
$titledisplay = readline("Enter Title Bar for Your HTML file => ");

if (!is_dir($directory)) {
    die("Error: Directory '$directory' does not exist.");
}

$handle = opendir($directory);
$videoList = [];

while (($file = readdir($handle)) !== false) {
    if (in_array($file, [".", ".."]) || !preg_match('/\.' . preg_quote($Exstention, '/') . '$/i', $file)) {
        continue;
    }

    $title = str_replace(".$Exstention", "", $file);
    $video = [
        "title" => $title,
        "source" => "$directory/$file",
    ];

    $found = false;
    foreach ($videoList as $item) {
        if (strtolower($item["title"]) === strtolower($title)) {
            $found = true;
            break;
        }
    }

    if (!$found) {
        $videoList[] = $video;
    }
}
closedir($handle);

$html = "<!DOCTYPE html>
<html lang=\"en\">
<head>
    <meta charset=\"UTF-8\">
    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\">
    <title>$titledisplay</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            text-transform: capitalize;
            font-family: 'Arial', sans-serif;
            font-weight: normal;
        }
        body {
            background: rgba(0, 0, 0, 1);
            color: rgba(255, 255, 255, 0.95);
        }
        .heading {
            color: #fff;
            font-size: 40px;
            text-align: center;
            padding: 20px;
            background: rgba(0, 0, 139, 0.45);
            text-shadow: 2px 2px 4px rgba(255, 255, 255, 1.25);
        }
        .container {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 20px;
            align-items: flex-start;
            padding: 20px 5%;
        }
        .container .main-video {
            background: rgba(0, 0, 139, 0.15);
            border-radius: 10px;
            padding: 15px;
            box-shadow: 0 4px 10px rgba(255, 255, 255, 1);
        }
        .container .main-video video {
            width: 100%;
            border-radius: 9px;
            aspect-ratio: 16 / 9;
            box-shadow: 0 2px 10px rgba(0, 127, 255, 0.5);
        }
        .container .main-video .title {
            color: rgba(255, 255, 255, 0.95);
            font-size: 24px;
            padding: 15px 0;
            text-align: center;
            font-weight: bold;
        }
        .container .video-list {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
            height: 720px;
            overflow-y: auto;
            padding: 10px;
            box-shadow: 0 4px 10px rgba(255, 255, 255, 0.35);
        }
        .container .video-list::-webkit-scrollbar {
            width: 8px;
        }
        .container .video-list::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.19);
            border-radius: 50px;
        }
        .container .video-list::-webkit-scrollbar-thumb {
            background: rgba(229, 9, 20, 0.75);
            border-radius: 50px;
        }
        .container .video-list .vid video {
            width: 100px;
            border-radius: 5px;
            aspect-ratio: 16 / 9;
        }
        .container .video-list .title {
            color: rgba(255, 255, 255, 0.95);
            font-size: 12px;
            text-align: center;
            margin-top: 1em;
        }
        .container .video-list .vid {
            display: flex;
            align-items: center;
            gap: 15px;
            background: rgba(0, 0, 51, 0.5);
            border-radius: 5px;
            margin: 10px 0;
            padding: 15px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            cursor: pointer;
            transition: background 0.3s;
            box-shadow: 0 2px 5px rgba(255, 255, 255, 1.15);
        }
        .container .video-list .vid:hover {
            background: rgba(0, 127, 255, 0.25);
        }
        .container .video-list .vid.active {
            background: rgba(229, 9, 20, 0.35);
        }

        button {
          background-color: rgba(0, 0, 51, 1);
          color: white;
          padding: 0.4em 1em;
          margin-top: 10px;
          border: none;
          border-radius: 5px;
          cursor: pointer;
          transition: background 0.3s;
          box-shadow: 0 1px 2px rgba(255, 255, 255, 1.25);
        }

        button:hover {
          background-color: rgba(229, 9, 20, 0.5);
        }

        .search-container {
          margin-bottom: 10px;
        }

        .search-container input {
          width: 100%;
          padding: 10px;
          border: none;
          border-radius: 5px;
          background-color: rgba(0, 72, 131, 0.25);
          color: rgba(255, 255, 255, 0.95);
          box-shadow: 0 2px 5px rgba(255, 255, 255, 1.15);
        }

        .theme-toggle {
            margin: 20px;
            cursor: pointer;
            padding: 10px;
            background-color: rgba(0, 127, 255, 0.5);
            border: none;
            border-radius: 5px;
            color: white;
        }

        @media (max-width: 991px) {
            .container {
                grid-template-columns: 2fr 1fr;
                padding: 10px;
            }
        }
        @media (max-width: 768px) {
            .container {
                grid-template-columns: 1fr;
                padding: 10px;
            }
        }

        .light-theme {
            background: #FFFFFF;
            color: rgba(0, 0, 0, 0.95);
        }
        .light-theme .container .main-video,
        .light-theme .container .video-list{
            background: rgba(0, 72, 131, 0.25);
            color: rgba(0, 0, 0, 0.95);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 1);
        }

        .light-theme .container .video-list .vid {
            box-shadow: 0 4px 10px rgba(0, 0, 0, 1);
        }
        .light-theme button {
            background-color: rgba(255, 255, 255, 1);
            color: rgba(0, 0, 0, 0.95);
            box-shadow: 0 1px 2px rgba(0, 0, 0, 0.25);
        }
        .light-theme button:hover {
            background-color: rgba(229, 9, 20, 0.5);
        }

        .light-theme .heading {
            color: #fff;
            font-size: 40px;
            text-align: center;
            padding: 20px;
            background: rgba(0, 72, 131, 0.25);
            text-shadow: 2px 2px 4px rgba(255, 255, 255, 1.25);
        }
        .light-theme .container .video-list .vid.active {
            background: rgba(229, 9, 20, 1);
        }

        .light-theme .container .video-list .vid:hover {
            background: rgba(0, 72, 131, 0.25);
            color: rgba(0, 72, 131, 0.15);
        }

        .light-theme .container .video-list::-webkit-scrollbar-track {
            background: rgba(0, 72, 131, 0.25);
        }

        .light-theme .container .video-list::-webkit-scrollbar-thumb {
            background: rgba(229, 9, 20, 1);
        }

    </style>
</head>
<body>
    <button class=\"theme-toggle\"> ☀ </button>
    <h3 class=\"heading\">$titledisplay</h3>
    <div class=\"container\">
        <div class=\"main-video\">
            <div class=\"video\">
                <video src=\"\" controls></video>
              </div>
              <div class=\"navigation-buttons\">
                <button id=\"prevButton\">⏮ Prev </button>
                <button id=\"nextButton\">Next ⏭</button>
                <button id=\"playPauseBtn\">Play</button>
                <button id=\"fullscreenBtn\">Fullscreen</button>
                <button id=\"volumeBtn\">🔊</button>
              </div>
              <h3 class=\"title\"></h3>
            </div>
        <div class=\"video-list\">
            <div class=\"search-container\">
            <input type=\"text\" id=\"searchInput\" placeholder=\"Search video title...\">
            </div>";

foreach ($videoList as $video) {
    $html .= "
            <div class=\"vid\">
                <video>
                    <source src=\"{$video["source"]}\" type=\"video/$Exstention\">
                    Your browser does not support the video tag.
                </video>
                <h3 class=\"title\">{$video["title"]}</h3>
            </div>";
}

$html .= "
        </div>
    </div>
      <script>
        let listVideo = document.querySelectorAll('.video-list .vid');
        let mainVideo = document.querySelector('.main-video video');
        let title = document.querySelector('.main-video .title');
        let currentIndex = 0;
        let searchInput = document.getElementById('searchInput');
        let durationDisplay = document.querySelector('.duration');

        function playVideo(index) {
          if (index >= 0 && index < listVideo.length) {
            listVideo.forEach(vid => vid.classList.remove('active'));
            listVideo[index].classList.add('active');
            if (listVideo[index].children[0].children[0].getAttribute('src')) {
              mainVideo.src = listVideo[index].children[0].children[0].getAttribute('src');
            }
            title.innerHTML = listVideo[index].children[1].innerHTML;
            currentIndex = index;
          }
        }

        listVideo.forEach((video, index) => {
          video.onclick = () => {
            playVideo(index);
          }
        });

        document.getElementById('prevButton').addEventListener('click', () => {
          playVideo(currentIndex - 1);
        });

        document.getElementById('nextButton').addEventListener('click', () => {
          playVideo(currentIndex + 1);
        });

        searchInput.addEventListener('input', function() {
          const searchTerm = this.value.toLowerCase();
          listVideo.forEach((video, index) => {
            const videoTitle = video.querySelector('.title').textContent.toLowerCase();
            if (videoTitle.includes(searchTerm)) {
              video.style.display = 'flex';
            } else {
              video.style.display = 'none';
            }
          });
        });

        const controls = document.querySelector('.controls');

        document.addEventListener('keydown', (event) => {
          switch (event.code) {
            case 'Space':
              event.preventDefault();
              mainVideo.paused ? mainVideo.play() : mainVideo.pause();
              break;
            case 'ArrowUp':
              mainVideo.volume = Math.min(mainVideo.volume + 0.1, 1);
              break;
            case 'ArrowDown':
              mainVideo.volume = Math.max(mainVideo.volume - 0.1, 0);
              break;
            case 'ArrowLeft':
              mainVideo.currentTime -= 5;
              break;
            case 'ArrowRight':
              mainVideo.currentTime += 5;
              break;
          }
        });

        const playPauseBtn = document.getElementById('playPauseBtn');
        const progressBar = document.querySelector('.progress');

        playPauseBtn.addEventListener('click', () => {
          if (mainVideo.paused) {
            mainVideo.play();
            playPauseBtn.textContent = 'Pause';
          } else {
            mainVideo.pause();
            playPauseBtn.textContent = 'Play';
          }
        });

        const fullscreenBtn = document.getElementById('fullscreenBtn');

        fullscreenBtn.addEventListener('click', () => {
          if (!document.fullscreenElement) {
            mainVideo.requestFullscreen();
          } else {
            document.exitFullscreen();
          }
        });

        const volumeBtn = document.getElementById('volumeBtn');
        volumeBtn.addEventListener('click', () => {
          mainVideo.muted = !mainVideo.muted;
          volumeBtn.textContent = mainVideo.muted ? '🔇' : '🔊';
        });

        const themeToggle = document.querySelector('.theme-toggle');
        themeToggle.addEventListener('click', () => {
          document.body.classList.toggle('light-theme');
        });

        // Play the first video initially
        playVideo(0);
      </script>
</body>
</html>";

$fileNamex = readline("Enter your file name *without .html* => ");
$fileName = "$fileNamex.html";
$filePath = "$directory/$fileName";

($fileHandle = fopen($filePath, "w")) or
    die("Error: Could not open file '$filePath' for writing.");
fwrite($fileHandle, $html);
fclose($fileHandle);

echo "\033[1;33mGenerated HTML file saved to: $filePath\033[0m";
?>
```

## Here The Screenshot

![video playlist galery](assets/img/Post/video-playlist-gallery/vgm1.gif)
![video playlist galery](assets/img/Post/video-playlist-gallery/vgm2.png)


## For Older Version

Visit My Github Repository Here : [SINGLE-FILE-HTML-OFFLINE-GALERY-OR-VIDEOS ](https://github.com/caturmahdialfurqon/SINGLE-FILE-HTML-OFFLINE-GALERY-OR-VIDEOS)

For New Release : [Update to version 1.0.1](https://github.com/caturmahdialfurqon/Video-Playlist-Gallery/releases/tag/single-html-gallery)