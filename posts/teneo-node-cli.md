---
title: Teneo Node CLI
date: 2024-10-17 14:48:05 +07:00
description: Running Teneo Node BETA, CLI Version with NodeJs ˗ˏˋ ★ ˎˊ˗
image : /assets/img/Post/Screenshot 2024-10-17 at 14.53.10.png
author: "cmalf"
---

# ᝰ.ᐟ TENEO-NODE

For More Detail Visit My github Repo [Teneo Node CLI](https://github.com/caturmahdialfurqon/TENEO-NODE-CLI)

Running Teneo Node BETA, CLI Version with NodeJs.
Teneo Is an Browser extension Node Based. <br>
<img src="https://cdn.prod.website-files.com/665c71122bb2018f6ed3f9c9/66eaaf8660d0ba047f3f2058_screenshot.png" loading="lazy" width="266" height="Auto" alt="" srcset="https://cdn.prod.website-files.com/665c71122bb2018f6ed3f9c9/66eaaf8660d0ba047f3f2058_screenshot-p-500.png 500w, https://cdn.prod.website-files.com/665c71122bb2018f6ed3f9c9/66eaaf8660d0ba047f3f2058_screenshot.png 626w" sizes="(max-width: 479px) 100vw, (max-width: 991px) 33vw, 266px" class="image-32"> <br>
Get paid in $TENEO Tokens for simply running a node that accesses public social media data. It’s easy, passive, and you earn from the value you contribute.



## 💡 How To SignUp (Register)

- Download the Extension
   - Teneo Community Node Extension -> [ teneo-community-node-v.0.2.zip ](https://teneo.pro/community-node#:~:text=Download%20extension%20as%20zip%20file%20teneo%2Dcommunity%2Dnode%2Dv.0.2.zip)
- Extract the Extension
   - Right click on the downloaded zip file and choose Extract All option. Make sure to select a convenient file destination, somewhere it won't be moved from after the install.
- Enable Developer Mode in Chrome or Other Browser Supported Extentions
   - Open the Extensions page in your Chrome: in the top right corner of your browser, click More> More tools > Extensions, or just type in chrome://extensions/ into your address bar. <br>
     Then, turn on     Developer mode switch in the top right corner.
- Load extension into Chrome
   - Locate the unzipped extension folder named teneo-community-node-v0.2 that contains manifest.json file. Drag and drop it anywhere onto the Extensions Chrome page to install.
- Pin it!
   - Click the extension puzzle icon next to the address bar and pin Teneo Community Node for quick access whenever you need to collect a lucrative lead!
- Open the Extention on browser Section, Click SignUp Button
- Create Account
- Enter Code : Wrsrs
- Verify Email
- Run Nodes Extension to Start earning rewards!
- Get 10000 Bonuse SignUp,And 2500 TENEO Point (Will Converted as $TENEO After TGE) When Using My Referal Code.

## `Source` CODE

```javascript
const WebSocket = require('ws');
const { promisify } = require('util');
const fs = require('fs');
const readline = require('readline');
const axios = require('axios');

let socket = null;
let pingInterval;
let countdownInterval;
let potentialPoints = 0;
let countdown = "Calculating...";
let pointsTotal = 0;
let pointsToday = 0;

const readFileAsync = promisify(fs.readFile);
const writeFileAsync = promisify(fs.writeFile);

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

async function getLocalStorage() {
  try {
    const data = await readFileAsync('localStorage.json', 'utf8');
    return JSON.parse(data);
  } catch (error) {
    return {};
  }
}

async function setLocalStorage(data) {
  const currentData = await getLocalStorage();
  const newData = { ...currentData, ...data };
  await writeFileAsync('localStorage.json', JSON.stringify(newData));
}

async function getUserIdFromFile() {
  try {
    const data = await readFileAsync('UserId.json', 'utf8');
    return JSON.parse(data).userId;
  } catch (error) {
    return null;
  }
}

async function setUserIdToFile(userId) {
  await writeFileAsync('UserId.json', JSON.stringify({ userId }));
}

async function getAccountData() {
  try {
    const data = await readFileAsync('DataAccount.json', 'utf8');
    return JSON.parse(data);
  } catch (error) {
    return {};
  }
}

async function setAccountData(email, password) {
  const accountData = { email, password };
  await writeFileAsync('DataAccount.json', JSON.stringify(accountData));
}

async function connectWebSocket(userId) {
  if (socket) return;
  const version = "v0.2";
  const url = "wss://secure.ws.teneo.pro";
  const wsUrl = `${url}/websocket?userId=${encodeURIComponent(userId)}&version=${encodeURIComponent(version)}`;
  socket = new WebSocket(wsUrl);

  socket.onopen = async () => {
    const connectionTime = new Date().toISOString();
    await setLocalStorage({ lastUpdated: connectionTime });
    console.log("WebSocket connected at", connectionTime);
    startPinging();
    startCountdownAndPoints();
  };

  socket.onmessage = async (event) => {
    const data = JSON.parse(event.data);
    console.log("Received message from WebSocket:", data);
    if (data.pointsTotal !== undefined && data.pointsToday !== undefined) {
      const lastUpdated = new Date().toISOString();
      await setLocalStorage({
        lastUpdated: lastUpdated,
        pointsTotal: data.pointsTotal,
        pointsToday: data.pointsToday,
      });
      pointsTotal = data.pointsTotal;
      pointsToday = data.pointsToday;
    }
  };

  socket.onclose = () => {
    socket = null;
    console.log("WebSocket disconnected");
    stopPinging();
    reconnectWebSocket();
  };

  socket.onerror = (error) => {
    console.error("WebSocket error:", error);
  };
}

function disconnectWebSocket() {
  if (socket) {
    socket.close();
    socket = null;
    stopPinging();
  }
}

function startPinging() {
  stopPinging();
  pingInterval = setInterval(async () => {
    if (socket && socket.readyState === WebSocket.OPEN) {
      socket.send(JSON.stringify({ type: "PING" }));
      await setLocalStorage({ lastPingDate: new Date().toISOString() });
    }
  }, 10000);
}

function stopPinging() {
  if (pingInterval) {
    clearInterval(pingInterval);
    pingInterval = null;
  }
}

process.on('SIGINT', () => {
  console.log('Received SIGINT. Stopping pinging...');
  stopPinging();
  disconnectWebSocket();
  process.exit(0);
});

function startCountdownAndPoints() {
  clearInterval(countdownInterval);
  updateCountdownAndPoints();
  countdownInterval = setInterval(updateCountdownAndPoints, 1000);
}

async function updateCountdownAndPoints() {
  const { lastUpdated } = await getLocalStorage();
  if (lastUpdated) {
    const nextHeartbeat = new Date(lastUpdated);
    nextHeartbeat.setMinutes(nextHeartbeat.getMinutes() + 15);
    const now = new Date();
    const diff = nextHeartbeat.getTime() - now.getTime();

    if (diff > 0) {
      const minutes = Math.floor(diff / 60000);
      const seconds = Math.floor((diff % 60000) / 1000);
      countdown = `${minutes}m ${seconds}s`;

      const maxPoints = 25;
      const timeElapsed = now.getTime() - new Date(lastUpdated).getTime();
      const timeElapsedMinutes = timeElapsed / (60 * 1000);
      let newPoints = Math.min(maxPoints, (timeElapsedMinutes / 15) * maxPoints);
      newPoints = parseFloat(newPoints.toFixed(2));

      if (Math.random() < 0.1) {
        const bonus = Math.random() * 2;
        newPoints = Math.min(maxPoints, newPoints + bonus);
        newPoints = parseFloat(newPoints.toFixed(2));
      }

      potentialPoints = newPoints;
    } else {
      countdown = "Calculating...";
      potentialPoints = 25;
    }
  } else {
    countdown = "Calculating...";
    potentialPoints = 0;
  }

  await setLocalStorage({ potentialPoints, countdown });
}

async function getUserId() {
  const loginUrl = "https://ikknngrgxuxgjhplbpey.supabase.co/auth/v1/token?grant_type=password";
  const authorization = "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imlra25uZ3JneHV4Z2pocGxicGV5Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3MjU0MzgxNTAsImV4cCI6MjA0MTAxNDE1MH0.DRAvf8nH1ojnJBc3rD_Nw6t1AV8X_g6gmY_HByG2Mag";
  const apikey = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imlra25uZ3JneHV4Z2pocGxicGV5Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3MjU0MzgxNTAsImV4cCI6MjA0MTAxNDE1MH0.DRAvf8nH1ojnJBc3rD_Nw6t1AV8X_g6gmY_HByG2Mag";

  const accountData = await getAccountData();
  const email = accountData.email || await new Promise(resolve => rl.question('Email: ', resolve));
  const password = accountData.password || await new Promise(resolve => rl.question('Password: ', resolve));

  try {
    const response = await axios.post(loginUrl, {
      email: email,
      password: password
    }, {
      headers: {
        'Authorization': authorization,
        'apikey': apikey
      }
    });

    const userId = response.data.user.id;
    console.log('User ID:', userId);

    const profileUrl = `https://ikknngrgxuxgjhplbpey.supabase.co/rest/v1/profiles?select=personal_code&id=eq.${userId}`;
    const profileResponse = await axios.get(profileUrl, {
      headers: {
        'Authorization': authorization,
        'apikey': apikey
      }
    });

    console.log('Profile Data:', profileResponse.data);
    await setUserIdToFile(userId);
    await setAccountData(email, password);
    await startCountdownAndPoints();
    await connectWebSocket(userId);
  } catch (error) {
    console.error('Error:', error.response ? error.response.data : error.message);
  } finally {
    rl.close();
  }
}

async function reconnectWebSocket() {
  const userId = await getUserIdFromFile();
  if (userId) {
    await connectWebSocket(userId);
  }
}

async function autoLogin() {
  const accountData = await getAccountData();
  if (accountData.email && accountData.password) {
    await getUserId();
  }
}

async function main() {
  const localStorageData = await getLocalStorage();
  let userId = await getUserIdFromFile();

  if (!userId) {
    rl.question('User ID not found. Would you like to:\n1. Login to your account\n2. Enter User ID manually\nChoose an option: ', async (option) => {
      switch (option) {
        case '1':
          await getUserId();
          break;
        case '2':
          rl.question('Please enter your user ID: ', async (inputUserId) => {
            userId = inputUserId;
            await setUserIdToFile(userId);
            await startCountdownAndPoints();
            await connectWebSocket(userId);
            rl.close();
          });
          break;
        default:
          console.log('Invalid option. Exiting...');
          process.exit(0);
      }
    });
  } else {
    rl.question('Menu:\n1. Logout\n2. Start Running Node\nChoose an option: ', async (option) => {
      switch (option) {
        case '1':
          fs.unlink('UserId.json', (err) => {
            if (err) throw err;
          });
          fs.unlink('localStorage.json', (err) => {
            if (err) throw err;
          });
          console.log('Logged out successfully.');
          process.exit(0);
          break;
        case '2':
          await startCountdownAndPoints();
          await connectWebSocket(userId);
          break;
        default:
          console.log('Invalid option. Exiting...');
          process.exit(0);
      }
    });
  }
}

main();
setInterval(autoLogin, 3600000);


```

## Release on my Github Repo

Teneo Node Update [New Release Teneo Node CLI](https://github.com/caturmahdialfurqon/TENEO-NODE-CLI/releases/tag/AutoReconnect-Teneo-Node)