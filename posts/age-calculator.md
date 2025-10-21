---
title: Age Calculator
date: 2024-10-28
description: This Script allows you to calculate age from any date.
image : assets/img/Post/math.gif
author: "cmalf"
---

# 📱 age-calculator

Javascript is used in this simple script to calculate the age of any date. <br> `Year, month, week, and day` will be used to display the calculated age.

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

const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// Coloring (Opstional), you can use chalk instead
const color = {
    green: '\x1b[32m',
    blue: '\x1b[34m',
    yellow: '\x1b[33m',
    underLine: '\x1b[4m',
    reset: '\x1b[0m'
};

function banner() {
    console.log(`
╭━━━╮╱╱╱╱╱╱╱╱╱╱╱╱╱╭━━━┳╮
┃╭━━╯╱╱╱╱╱╱╱╱╱╱╱╱╱┃╭━━┫┃${color.green}Age
┃╰━━┳╮╭┳━┳━━┳━━┳━╮┃╰━━┫┃╭╮╱╭┳━╮╭━╮
┃╭━━┫┃┃┃╭┫╭╮┃╭╮┃╭╮┫╭━━┫┃┃┃╱┃┃╭╮┫╭╮╮
┃┃╱╱┃╰╯┃┃┃╰╯┃╰╯┃┃┃┃┃╱╱┃╰┫╰━╯┃┃┃┃┃┃┃
╰╯╱╱╰━━┻╯╰━╮┣━━┻╯╰┻╯╱╱╰━┻━╮╭┻╯╰┻╯╰╯
╱╱╱╱╱╱╱╱╱╱╱┃┃╱╱╱╱╱╱╱╱╱╱╱╭━╯┃${color.green}calculator${color.reset}
╱╱╱╱╱╱╱╱╱╱╱╰╯╱╱╱╱╱╱╱╱╱╱╱╰━━╯
    `);
}
// Logic
function calculateAge(fromDate, toDate) {
    const endDate = toDate ? new Date(toDate) : new Date();
    const birthDate = new Date(fromDate.slice(0, 4), fromDate.slice(4, 6) - 1, fromDate.slice(6, 8));
    
    let ageYears = endDate.getFullYear() - birthDate.getFullYear();
    let ageMonths = endDate.getMonth() - birthDate.getMonth();
    let ageDays = endDate.getDate() - birthDate.getDate();

    if (ageDays < 0) {
        ageMonths--;
        const lastMonth = new Date(endDate.getFullYear(), endDate.getMonth(), 0);
        ageDays += lastMonth.getDate();
    }

    if (ageMonths < 0) {
        ageYears--;
        ageMonths += 12;
    }

    const fullMonths = ageYears * 12 + ageMonths;
    const totalDays = Math.floor((endDate - birthDate) / (1000 * 60 * 60 * 24));
    const weeks = Math.floor(totalDays / 7);

    return {
        years: ageYears,
        months: ageMonths,
        days: ageDays,
        fullMonths: fullMonths,
        weeks: weeks,
        totalDays: totalDays
    };
}

function printResult(result) {
    console.log(`${color.reset}${color.underLine}\nResult of ${color.green}age calculation${color.reset}`);
    console.log(`${color.reset}\nAge         : ${color.green}${result.years} year(s) ${result.months} month(s) ${result.days} day(s)${color.reset}`);
    console.log(`${color.reset}Full months : ${color.green}${result.fullMonths} month(s)${color.reset}`);
    console.log(`${color.reset}Weeks       : ${color.green}${result.weeks} weeks${color.reset}`);
    console.log(`${color.reset}Days        : ${color.green}${result.totalDays} day(s)${color.reset}\n`);
}

function continueOrExit(fromDate, toDate) {
    rl.question('Do you want to continue using the script? (y/n): ', (answer) => {
        if (answer.toLowerCase() === 'y') {
            start();
        } else {
            console.log(`${color.green}Thank you!${color.reset}`);
            rl.close();
        }
    });
}

function start() {
    rl.question(`${color.yellow}Enter From date (YYYYMMDD)${color.reset}: `, (fromDate) => {
        rl.question(`${color.yellow}To date${color.reset} ("1" for ${color.green}today${color.reset} or "2" for${color.green} custom date${color.reset}): `, (toDateInput) => {
            let toDate;
            if (toDateInput === '1') {
                toDate = new Date();
            } else if (toDateInput === '2') {
                rl.question(`${color.yellow}Enter From date (YYYYMMDD)${color.reset}: `, (customDate) => {
                    toDate = new Date(customDate.slice(0, 4), customDate.slice(4, 6) - 1, customDate.slice(6, 8));
                    const result = calculateAge(fromDate, toDate);
                    printResult(result);
                    continueOrExit(fromDate, toDate);
                });
                return;
            } else {
                toDate = new Date(toDateInput.slice(0, 4), toDateInput.slice(4, 6) - 1, toDateInput.slice(6, 8));
            }

            const result = calculateAge(fromDate, toDate);
            printResult(result);
            continueOrExit(fromDate, toDate);
        });
    });
}

console.clear();
banner();
start();

```


`For more Detail` on my github repo [Age-calculator](https://github.com/caturmahdialfurqon/age-calculator)

## [◉°] ScreenShot

![agecalc](assets/img/Post/age-calculator/Screenshot 2024-10-28 at 02.53.25.png){: w="700" h="680" }

