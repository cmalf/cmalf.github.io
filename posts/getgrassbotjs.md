---
title: 🌱 getgrass-miner-bot
date: 2024-12-09 21:21:28 +07:00
description: A Node.js script to automate grass Season 2 mining.
image: /assets/img/Post/getgrassbot.png
author: "cmalf"
---

# 🌱 grass-miner-js
## Update on release section!
  - Release [grass-desktop-v0.2](https://github.com/cmalf/grass-miner-js/releases/tag/grass-desktop-v0.2)
  - mining 2.00X
  - more stable
  - bug fixed
<hr><br><br>
- `Season 2` <br>
This Javascript-based script will automate grass node mining while managing multiple devices and IP addresses to maximize profits and maintain sustainable uptime. Ideal for people who want to manage WebSocket connections using the SOCKS5 Protocol smoothly and effectively. <br>
                -
                  - <img src="https://github.com/user-attachments/assets/139f163e-f202-4621-a6fb-39d9c1f2f388" width="600" height="300" alt="Screenshot">


## 🔓 Register 
if you don't have a grass account yet, SignUp Here [getgrass.io](https://app.getgrass.io/register/?referralCode=wDYQ8wpucFyJaAU)

## 🤔 How To Do
- Clone This Repo
  - ```bash
    git clone https://github.com/cmalf/grass-miner-js.git
    ```
- Go To Folder
  - ```bash
    cd grass-miner-js
    ```
- Install Dependencies
  - ```bash
    npm install
    ```
## ⚙️ Configuration

SetUp on `Configuration.js`

- Get UserId
  - Login to your grass account
  - Go to Dashboard
  - Inspect Element
  - Type `localStorage.getItem('userId')` in the console
  - or just Click Here [get UserId](https://api.getgrass.io/retrieveUser) make sure you have been logged into grass dashboard
    - ![Screenshot 2024-11-11 at 07 36 24](https://github.com/user-attachments/assets/6fd576ab-b730-473a-8072-2cdb1a54df4e)
- Get Extention Id
  - Go To [chrome://extensions/](chrome://extensions/)
  - <img src="https://github.com/user-attachments/assets/58c8116c-3e99-43c7-be4a-0849c0428d37" width="650" height="350" alt="Screenshot">
- Get Useragent Click [Here](https://ipchicken.com/)
  - <img src="https://github.com/user-attachments/assets/8b64ab22-d308-4ee5-854d-58ac275768fb" width="650" height="250" alt="Screenshot">

- Edit Proxy.txt
  - format proxies is: `socks5://username:pass@ip:port`

- 🏃🏻‍♂️‍➡️ Run The Script
  - if the configuration is complete
  ```bash
  node main.js
  ```
  - <img src="https://github.com/user-attachments/assets/a65a126b-d899-4818-9fd2-8689480bbcb4" widht=580 height=480 >

## 📢 Additional information

  To get a stable Proxy you can use this Platform, plans ranging from $3 to $125 for 6 months, or use your own choice.
  
- Get Proxies IP address Socks5
  - Create an account at [proxies.fo](https://app.proxies.fo/ref/8b1abd0f-c734-1602-5985-612caedf4c7b)
  - Go to `purchase isp`  and `buy` a plan according to `your needs`.
    - You can use `cryptocurrency` for `payment` 
    - <img src="https://github.com/user-attachments/assets/18f24ed1-cfc6-4141-addb-07e009c7226b" width="720" height="480" alt="Screenshot">
  - after that you go to the dashboard `Click Generate proxy Button`
  - Now You can change the Proxy format to :
     - `protocol://username:password@hostname:port`
     - or just look the ss below
     - ![Screenshot 2024-12-06 at 16 24 31](https://github.com/user-attachments/assets/c9d552f1-7241-4705-8580-30a88aae8638)




