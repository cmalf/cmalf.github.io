---
title: RegEx-Tester
date: 2024-10-30 00:54:42 +07:00
description: This free RegEX tester lets you test your regular expressions.
image : assets/img/Post/regex.jpg
author: "cmalf"
---

# ⚙️🇷 RegEx-Tester

This free RegEX tester lets you test your regular expressions.

## `Source` CODE

```javascript
#!/usr/bin/env node

// MIT License

// Copyright (c) 2024 Furqonflynn

// Permission is hereby granted, free of charge, to any person obtaining a copy
// of this software and associated documentation files (the "Software"), to deal
// in the Software without restriction, including without limitation the rights
// to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
// copies of the Software, and to permit persons to whom the Software is
// furnished to do so, subject to the following conditions:

// The above copyright notice and this permission notice shall be included in all
// copies or substantial portions of the Software.

// THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
// IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
// FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
// AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
// LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
// OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
// SOFTWARE.

const fs = require('fs');
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Coloring (Opstional), you can use chalk instead
const color = {
    green: '\x1b[32m',
    red: '\x1b[31m',
    blue: '\x1b[34m',
    yellow: '\x1b[33m',
    underLine: '\x1b[4m',
    reset: '\x1b[0m'
};

function banner() {
    console.log(`
╭━━━╮╱╱╱╱╱╱╱╱╱╱╱╱╱╭━━━┳╮
┃╭━━╯╱╱╱╱╱╱╱╱╱╱╱╱╱┃╭━━┫┃${color.yellow}RegExp${color.green}
┃╰━━┳╮╭┳━┳━━┳━━┳━╮┃╰━━┫┃╭╮╱╭┳━╮╭━╮
┃╭━━┫┃┃┃╭┫╭╮┃╭╮┃╭╮┫╭━━┫┃┃┃╱┃┃╭╮┫╭╮╮
┃┃╱╱┃╰╯┃┃┃╰╯┃╰╯┃┃┃┃┃╱╱┃╰┫╰━╯┃┃┃┃┃┃┃
╰╯╱╱╰━━┻╯╰━╮┣━━┻╯╰┻╯╱╱╰━┻━╮╭┻╯╰┻╯╰╯
╱╱╱╱╱╱╱╱╱╱╱┃┃╱╱╱╱╱╱╱╱╱╱╱╭━╯┃${color.red}Tester${color.reset}
╱╱╱╱╱╱╱╱╱╱╱╰╯╱╱╱╱╱╱╱╱╱╱╱╰━━╯
        `);
}

const menu = `
1. ${color.green}${color.underLine}Check Regex${color.reset}
2. ${color.underLine}Examples${color.reset}
3. ${color.reset}Settings
4. ${color.red}Exit${color.reset}
\nEnter Your choice: `;

function promptUser() {
    rl.question(menu, (choice) => {
        switch (choice) {
            case '1':
                checkRegex();
                break;
            case '2':
                showExamples();
                break;
            case '3':
                console.clear();
                settingsMenu();
                break;
            case '4':
                rl.close();
                break;
            default:
                console.log('Invalid choice. Please try again.');
                promptUser();
        }
    });
}
//Checking input string type Before Execute Regextester 
function checkRegex() {
    rl.question(`${color.yellow}Enter the regex pattern${color.reset}: `, (pattern) => {
        const settings = JSON.parse(fs.readFileSync('settings.json', 'utf8'));
        if (settings.TestStringsInput) {
            console.log(`${color.blue}=> Multiple Test Strings${color.reset} `);
            enterTestStrings(pattern);
        } else {
            console.log(`${color.blue}=> Single Test Strings${color.reset} `);
            rl.question(`${color.yellow}Enter the string to test${color.reset}: `, (testString) => {
                executeRegex(pattern, testString, settings);
            });
        }
    });
}
//Executing String for testing
function executeRegex(pattern, testString, settings) {
    try {
        const flags = `${settings.caseInsensitive ? 'i' : ''}${settings.global ? 'g' : ''}${settings.multiline ? 'm' : ''}${settings.dotMatchesAll ? 's' : ''}`;
        const regex = new RegExp(pattern, flags);
        const matches = testString.match(regex);
        const result = matches ? `${color.blue}True${color.reset} Found ${matches.length} matches.` : `${color.red}False${color.reset} Not Found matches`;
        console.log(`${color.yellow}Result${color.reset}: ${result}`);
        if (matches) {
            const highlightedString = testString.replace(regex, (match) => `${color.green}${color.underLine}${match}${color.reset}`);
            console.log(`${color.yellow}Matches are Underline below${color.reset}:\n${highlightedString}\n`);
        }
    } catch (e) {
        console.log(`${color.red}Invalid regex pattern. Please try again.${color.reset}`);
    }
    continueOrExit();
}

function continueOrExit() {
    rl.question('Do you want to continue using the script? (y/n): ', (answer) => {
        if (answer.toLowerCase() === 'y') {
            checkRegex();
        } else {
            console.log(`${color.green}Thank you!${color.reset}`);
            rl.close();
        }
    });
}
// Showing Examples
function showExamples() {
    console.log(`
Examples:
1. Pattern: ^[a-z]+$ | String: hello | Result: true
2. Pattern: \\d+ | String: 123abc | Result: true
3. Pattern: \\w+@\\w+\\.\\w+ | String: test@example.com | Result: true
`);
    continueOrExit();
}
// Setting Flag and Input String Type
function settingsMenu() {
    console.log(`
(1 for true/ 0 for false)\n
 i - Case-insensitive 
 m - Multiline 
 g - Global (don't stop at first match) 
 s - Dot matches all INCLUDING line breaks\n 
 Test Strings (1 for Multiple Input) \n `);
    
    rl.question('Case-insensitive (1/0): ', (caseInsensitive) => {
        rl.question('Multiline (1/0): ', (multiline) => {
            rl.question('Global (1/0): ', (global) => {
                rl.question('Dot matches all (1/0): ', (dotMatchesAll) => {
                    rl.question('\nTestStringsInput (1/0): ', (TestStringsInput) => {
                        const settings = {
                            caseInsensitive: caseInsensitive === '1',
                            multiline: multiline === '1',
                            global: global === '1',
                            dotMatchesAll: dotMatchesAll === '1',
                            TestStringsInput: TestStringsInput === '1',
                        };
                        fs.writeFileSync('settings.json', JSON.stringify(settings, null, 2));
                        console.clear();
                        console.log('Settings saved to settings.json');
                        promptUser();
                    });
                });
            });
        });
    });
}
// Multiple Input String Test
function enterTestStrings(pattern) {
    const testStrings = [];
    console.log(`${color.yellow}Enter the string to test${color.blue} (or type "done" to finish)${color.reset}:`);
    
    function getTestString() {
        rl.question(`${color.green}(>${color.reset} `, (testString) => {
            if (testString.toLowerCase() === 'done') {
                const settings = JSON.parse(fs.readFileSync('settings.json', 'utf8'));
                const combinedTestString = testStrings.join('\n');
                executeRegex(pattern, combinedTestString, settings);
                continueOrExit();
            } else {
                testStrings.push(testString);
                getTestString();
            }
        });
    }
    getTestString();
}

if (!fs.existsSync('settings.json')) {
    console.clear();
    console.log(`${color.red}settings.json not found. Defaulting to settings option.${color.reset}`);
    settingsMenu();
} else {
    console.clear();
    banner();
    promptUser();
}

```

`For more Detail` on my github repo [Regex-Tester](https://github.com/caturmahdialfurqon/RegEx-Tester)

## [◉°] ScreenShot

- The first time you run the script it will automatically go to the settings menu.

![regex](assets/img/Post/regex/Screenshot 2024-10-28 at 03.59.56.png){: w="700" h="680" }

- Single String Input

![regex1](assets/img/Post/regex/Screenshot 2024-10-28 at 03.55.20.png){: w="700" h="680" }

- Multiple String Input

![regex2](assets/img/Post/regex/Screenshot 2024-10-28 at 03.44.22.png){: w="700" h="680" }