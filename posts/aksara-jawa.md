---
title: Javanese Script Alphabet
date: 2024-10-26
description: Translate from Latin Script to Javanese Script.
image : assets/img/Post/javanese.jpg
author: "cmalf"
---

# Javanese (Script) Alphabet

This script can be used to translate or change words or sentences from Latin script to Javanese script

## `Source` CODE

```javascript
#!/usr/bin/env node

//###################################################################################################//
// Code Rewriting To JavaScript By FurqonFlynn `https://github.com/caturmahdialfurqon/Aksara-Jawa``  //
// From Python By lantip `https://github.com/lantip/latintojavanese``                                       //
//###################################################################################################//

const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

const warna = {
    hijau: '\x1b[32m',
    biru: '\x1b[34m',
    garisBawah: '\x1b[4m',
    reset: '\x1b[0m'
};

// Ctrl + C
process.on('SIGINT', () => {
     rl.close();
     process.exit(0);
});


let bannerPrinted = false;
let ModeribetkkkPrinted = false;


function banner() {
    if (!bannerPrinted) {
    console.log(`
╭━━━╮╱╱╱╱╱╱╱╱╱╱╱╱╱╭━━━┳╮Terjemahkan
┃╭━━╯╱╱╱╱╱╱╱╱╱╱╱╱╱┃╭━━┫┃${warna.biru}Latin${warna.reset}
┃╰━━┳╮╭┳━┳━━┳━━┳━╮┃╰━━┫┃╭╮╱╭┳━╮╭━╮
┃╭━━┫┃┃┃╭┫╭╮┃╭╮┃╭╮┫╭━━┫┃┃┃╱┃┃╭╮┫╭╮╮
┃┃╱╱┃╰╯┃┃┃╰╯┃╰╯┃┃┃┃┃╱╱┃╰┫╰━╯┃┃┃┃┃┃┃
╰╯╱╱╰━━┻╯╰━╮┣━━┻╯╰┻╯╱╱╰━┻━╮╭┻╯╰┻╯╰╯
╱╱╱╱╱╱╱╱╱╱╱┃┃╱╱╱╱╱╱╱╱╱╱╱╭━╯┃Ke
╱╱╱╱╱╱╱╱╱╱╱╰╯╱╱╱╱╱╱╱╱╱╱╱╰━━╯${warna.hijau}Aksara jawa
\n${warna.biru}Ketik quit atau Ctrl+C Untuk Keluar...${warna.reset}
        `);
        bannerPrinted = true;
    }
}

function Moderibetkkk(){
    if (!ModeribetkkkPrinted) {
    console.log(`${warna.garisBawah}Masukan Kata Atau Kalimat :\n`);
            ModeribetkkkPrinted = true;
    }
}


const HURUF = {
    'h': 'ꦲ',
    'n': 'ꦤ',
    'c': 'ꦕ',
    'r': 'ꦫ',
    'k': 'ꦏ',
    'd': 'ꦢ',
    't': 'ꦠ',
    's': 'ꦱ',
    'w': 'ꦮ',
    'l': 'ꦭ',
    'p': 'ꦥ',
    'dh': 'ꦝ',
    'j': 'ꦗ',
    'y': 'ꦪ',
    'ny': 'ꦚ',
    'm': 'ꦩ',
    'g': 'ꦒ',
    'b': 'ꦧ',
    'th': 'ꦛ',
    'ng': 'ꦔ',
    ',': '꧈',
    '.': '꧉'
};

const PASANGAN = {
    'h': '꧀ꦲ',
    'n': '꧀ꦤ',
    'c': '꧀ꦕ',
    'r': '꧀ꦫ',
    'k': '꧀ꦏ',
    'd': '꧀ꦢ',
    't': '꧀ꦠ',
    's': '꧀ꦱ',
    'w': '꧀ꦮ',
    'l': '꧀ꦭ',
    'p': '꧀ꦥ',
    'dh': '꧀ꦓ',
    'j': '꧀ꦗ',
    'y': '꧀ꦪ',
    'ny': '꧀ꦚ',
    'm': '꧀ꦩ',
    'g': '꧀ꦒ',
    'b': '꧀ꦧ',
    'th': '꧀ꦛ',
    'ng': '꧀ꦔ'
};

const SANDHANGAN = {
    'wulu': 'ꦶ',
    'suku': 'ꦸ',
    'pepet': 'ꦼ',
    'taling': 'ꦺ',
    'taling-tarung': 'ꦺꦴ',
    'cecak': 'ꦁ',
    'wignyan': 'ꦃ',
    'layar': 'ꦂ',
    'cakra': 'ꦿ',
    'keret': 'ꦽ',
    'pengkal': 'ꦾ',
    'pangkon': '꧀'
};

function transliterate(hrf, isend, prv, nxt) {
    let ltr = '';
    const dobel = ['th', 'dh', 'ny'];
    let iskeret = false;
    if (hrf.indexOf('ng') === 0) {
        if (hrf.length === 2) {
            ltr += SANDHANGAN['cecak'];
        } else {
            ltr += HURUF['ng'];
        }
        if (hrf.length > 3) {
            if (hrf[2] === 'l') {
                ltr += PASANGAN['l'];
            } else if (hrf[2] === 'y') {
                ltr += SANDHANGAN['pengkal'];
            } else if (hrf[2] === 'r') {
                if (hrf[3] === 'e') {
                    ltr += SANDHANGAN['keret'];
                    iskeret = true;
                } else {
                    ltr += SANDHANGAN['cakra'];
                }
            }
        }
    } else if (hrf.indexOf('ny') === 0) {
        if (prv) {
            if (prv.length === 1) {
                ltr += PASANGAN['ny'];
            } else {
                ltr += HURUF['ny'];
            }
        } else {
            ltr += HURUF['ny'];
        }
        if (hrf.length > 3) {
            if (hrf[2] === 'l') {
                ltr += PASANGAN['l'];
            } else if (hrf[2] === 'y') {
                ltr += SANDHANGAN['pengkal'];
            } else if (hrf[2] === 'r') {
                if (hrf[3] === 'e') {
                    ltr += SANDHANGAN['keret'];
                    iskeret = true;
                } else {
                    ltr += SANDHANGAN['cakra'];
                }
            }
        }
    } else if (hrf.indexOf('th') === 0) {
        if (prv) {
            if (prv.length === 1) {
                ltr += PASANGAN['th'];
            } else {
                ltr += HURUF['th'];
            }
        } else {
            ltr += HURUF['th'];
        }
        if (hrf.length > 3) {
            if (hrf[2] === 'l') {
                ltr += PASANGAN['l'];
            } else if (hrf[2] === 'y') {
                ltr += SANDHANGAN['pengkal'];
            } else if (hrf[2] === 'r') {
                if (hrf[3] === 'e') {
                    ltr += SANDHANGAN['keret'];
                    iskeret = true;
                } else {
                    ltr += SANDHANGAN['cakra'];
                }
            }
        }
    } else if (hrf.indexOf('dh') === 0) {
        if (prv) {
            if (prv.length === 1) {
                ltr += PASANGAN['dh'];
            } else {
                ltr += HURUF['dh'];
            }
        } else {
            ltr += HURUF['dh'];
        }
        if (hrf.length > 3) {
            if (hrf[2] === 'l') {
                ltr += PASANGAN['l'];
            } else if (hrf[2] === 'y') {
                ltr += SANDHANGAN['pengkal'];
            } else if (hrf[2] === 'r') {
                if (hrf[4] === 'e') {
                    ltr += SANDHANGAN['keret'];
                    iskeret = true;
                } else {
                    ltr += SANDHANGAN['cakra'];
                }
            }
        }
    }
    if (hrf.length === 2) {
        if (hrf === 'ng') {
            ltr += SANDHANGAN['cecak'];
        } else {
            if (prv) {
                if (prv.length === 1) {
                    if (!['h', 'r', 'y'].includes(prv)) {
                        ltr += PASANGAN[hrf[0]];
                    } else {
                        ltr += HURUF[hrf[0]];
                    }
                } else {
                    ltr += HURUF[hrf[0]];
                }
            } else {
                ltr += HURUF[hrf[0]];
            }
        }
    } else if (hrf.length === 1) {
        if (![',', '.'].includes(hrf[0])) {
            if (hrf === 'r') {
                ltr += SANDHANGAN['layar'];
            } else if (hrf === 'h') {
                ltr += SANDHANGAN['wignyan'];
            } else if (hrf === ',') {
                // pass
            } else {
                if (isend) {
                    ltr += HURUF[hrf[0]];
                    ltr += SANDHANGAN['pangkon'];
                } else {
                    ltr += HURUF[hrf[0]];
                }
            }
        }
    } else if (hrf.length > 2) {
        if (hrf[1] === 'l') {
            ltr += HURUF[hrf[0]];
            ltr += PASANGAN['l'];
        } else if (hrf[1] === 'y' && hrf[0] !== 'n') {
            ltr += HURUF[hrf[0]];
            ltr += SANDHANGAN['pengkal'];
        } else if (hrf[1] === 'r') {
            if (prv) {
                if (prv.length === 1) {
                    if (!['h', 'r', 'y'].includes(prv)) {
                        ltr += PASANGAN[hrf[0]];
                        ltr += SANDHANGAN['cakra'];
                    } else {
                        ltr += HURUF[hrf[0]];
                        ltr += SANDHANGAN['cakra'];
                    }
                } else {
                    ltr += HURUF[hrf[0]];
                    ltr += SANDHANGAN['cakra'];
                }
            } else {
                ltr += HURUF[hrf[0]];
                ltr += SANDHANGAN['cakra'];
            }
        }
    }
    if (hrf.indexOf('u') === hrf.length - 1) {
        ltr += SANDHANGAN['suku'];
    }

    if (hrf.includes('é') || hrf.includes('è')) {
        if (prv) {
            ltr += SANDHANGAN['taling'];
        } else {
            ltr += SANDHANGAN['taling'];
        }
    }
    if (hrf.indexOf('e') === hrf.length - 1) {
        if (!iskeret) {
            ltr += SANDHANGAN['pepet'];
        }
    }
    if (hrf.indexOf('i') === hrf.length - 1) {
        ltr += SANDHANGAN['wulu'];
    }
    if (hrf.includes('o')) {
        ltr += SANDHANGAN['taling-tarung'];
    }
    if (nxt === '.') {
        ltr += HURUF[nxt];
    }
    return ltr;
}

function translate(word) {
    let ltr = [];
    let start = 0;
    const consonant = ['c','k','s','w','l','p','j','m','b'];
    const specials = ['t','d'];
    const dobel = ['th', 'dh', 'ny', 'ng'];
    const insrt = ['h','y','g','n'];
    const vowels = "AaEeÈèÉéIiOoUuÊêĚěĔĕṚṛXxôâāīūō";
    for (let dob of dobel) {
        if (word.indexOf(dob) === 0) {
            if (word.length >= 3) {
                if (vowels.includes(word[2])) {
                    ltr.push(dob + word[2]);
                    start = 3;
                }
            } else if (word.length >= 4) {
                if (word[2] === 'r') {
                    if (vowels.includes(word[3])) {
                        ltr.push(dob + 'r' + word[3]);
                        start = 4;
                    }
                }
            }
        }
    }
    for (let ins of insrt) {
        if (word.indexOf(ins) === 0) {
            if (word.length >= 2) {
                if (vowels.includes(word[1])) {
                    ltr.push(ins + word[1]);
                    start = 2;
                } else if (['l', 'r', 'y'].includes(word[1])) {
                    if (vowels.includes(word[2])) {
                        ltr.push(ins + word[1] + word[2]);
                        start = 3;
                    }
                }
            }
        }
    }
    if (vowels.includes(word[0])) {
        ltr.push('h' + word[0]);
        start = 1;
    }
    for (let i = start; i < word.length; i++) {
        if (consonant.includes(word[i])) {
            try {
                if (word.slice(i).length > 1) {
                    if (vowels.includes(word[i + 1]) && word[i] !== 'l') {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    } else {
                        if (['l', 'r', 'y'].includes(word[i + 1])) {
                            if (word.slice(i).length > 2) {
                                if (vowels.includes(word[i + 2])) {
                                    ltr.push(word[i] + word[i + 1] + word[i + 2]);
                                    i += 3;
                                } else {
                                    ltr.push(word[i] + word[i + 1]);
                                    i += 2;
                                }
                            } else {
                                if (i - 2 >= 0) {
                                    if (word.slice(i).length > 1) {
                                        if (!word.slice(i - 2, i).includes(word[i])) {
                                            ltr.push(word[i] + word[i + 1]);
                                            i += 2;
                                        }
                                    }
                                }
                            }
                        } else {
                            if (word[i] !== 'l') {
                                ltr.push(word[i]);
                                i += 1;
                            } else {
                                if (word.slice(i).length > 1) {
                                    if (vowels.includes(word[i + 1])) {
                                        if (ltr.length > 0) {
                                            if (!ltr[ltr.length - 1].includes(word[i] + word[i + 1])) {
                                                ltr.push(word[i] + word[i + 1]);
                                                i += 2;
                                            }
                                        } else {
                                            ltr.push(word[i] + word[i + 1]);
                                            i += 2;
                                        }
                                    }
                                }
                            }
                        }
                    }
                } else {
                    ltr.push(word[i]);
                    i += 1;
                }
            } catch (e) {
                ltr.push(word[i]);
                i += 1;
            }
        } else if (specials.includes(word[i])) {
            try {
                if (word.slice(i).length >= 2) {
                    if (word[i + 1] === 'h' && vowels.includes(word[i + 2])) {
                        ltr.push(word[i] + word[i + 1] + word[i + 2]);
                        i += 3;
                    } else if (['l', 'r'].includes(word[i + 1])) {
                        if (word.slice(i).length > 2) {
                            if (vowels.includes(word[i + 2])) {
                                ltr.push(word[i] + word[i + 1] + word[i + 2]);
                                i += 3;
                            } else {
                                ltr.push(word[i] + word[i + 1]);
                                i += 2;
                            }
                        } else {
                            ltr.push(word[i] + word[i + 1]);
                            i += 2;
                        }
                    } else if (vowels.includes(word[i + 1])) {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    }
                } else if (word.slice(i).length === 1) {
                    if (word[i + 1] === 'h') {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    } else if (vowels.includes(word[i + 1])) {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    }
                }
            } catch (e) {
                ltr.push(word[i]);
                i += 1;
            }
        } else if (word[i] === 'n') {
            if (word.slice(i).length > 2) {
                if (['g', 'y'].includes(word[i + 1]) && vowels.includes(word[i + 2])) {
                    ltr.push(word[i] + word[i + 1] + word[i + 2]);
                    i += 3;
                } else if (['g', 'y'].includes(word[i + 1]) && !vowels.includes(word[i + 2])) {
                    ltr.push(word[i] + word[i + 1]);
                    i += 2;
                } else {
                    if (vowels.includes(word[i + 1])) {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    } else {
                        ltr.push(word[i]);
                        i += 1;
                    }
                }
            } else {
                try {
                    let nxt = word[i + 1];
                } catch (e) {
                    nxt = null;
                }
                if (nxt) {
                    if (vowels.includes(nxt)) {
                        ltr.push(word[i] + nxt);
                        i += 2;
                    } else if (nxt === 'g') {
                        ltr.push(word[i] + nxt);
                        i += 2;
                    } else {
                        ltr.push(word[i]);
                        i += 1;
                    }
                } else {
                    ltr.push(word[i]);
                    i += 1;
                }
            }
        } else if (['r', 'y'].includes(word[i])) {
            if (i === 0) {
                if (word.slice(i).length > 1) {
                    if (vowels.includes(word[i + 1])) {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    }
                }
            } else {
                if (word.slice(i).length > 1) {
                    if (vowels.includes(word[i + 1])) {
                        if (!vowels.includes(word[i - 1])) {
                            if (i - 2 >= 0) {
                                if (dobel.includes(word[i - 2] + word[i - 1])) {
                                    ltr.push(word[i - 2] + word[i - 1] + word[i] + word[i + 1]);
                                    i += 2;
                                } else {
                                    if (!ltr[ltr.length - 1].includes(word[i] + word[i + 1])) {
                                        ltr[ltr.length - 1] += word[i] + word[i + 1];
                                        i += 1;
                                    }
                                }
                            } else {
                                ltr.push(word[i] + word[i + 1]);
                                i += 2;
                            }
                        } else {
                            ltr.push(word[i] + word[i + 1]);
                            i += 2;
                        }
                    } else {
                        ltr.push(word[i]);
                        i += 1;
                    }
                } else {
                    ltr.push(word[i]);
                    i += 1;
                }
            }
        } else if (word[i] === 'g') {
            if (ltr[ltr.length - 1].includes('g') && ltr[ltr.length - 1].length >= 2) {
                // pass
            } else {
                if (word.slice(i).length > 1) {
                    if (vowels.includes(word[i + 1])) {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    } else {
                        if (i - 2 > 0) {
                            if (word[i - 2] + word[i - 1] === 'ng') {
                                // pass
                            } else {
                                if (ltr[ltr.length - 1] !== 'ng') {
                                    ltr.push(word[i]);
                                    i += 1;
                                } else {
                                    i += 1;
                                }
                            }
                        } else {
                            if (ltr[ltr.length - 1] !== 'ng') {
                                ltr.push(word[i]);
                                i += 1;
                            } else {
                                i += 1;
                            }
                        }
                    }
                } else {
                    if (i - 2 > 0) {
                        if (word[i - 2] + word[i - 1] === 'ng') {
                            // pass
                        } else if (word[i - 1] + word[i] === 'ng') {
                            // pass
                        } else {
                            ltr.push(word[i]);
                            i += 1;
                        }
                    } else {
                        ltr.push(word[i]);
                        i += 1;
                    }
                }
            }
        } else if (word[i] === 'h') {
            if (ltr[ltr.length - 1].includes('h') && ltr[ltr.length - 1].length > 2) {
                // pass
            } else {
                if (word.slice(i).length > 1) {
                    if (vowels.includes(word[i + 1])) {
                        ltr.push(word[i] + word[i + 1]);
                        i += 2;
                    } else {
                        ltr.push(word[i]);
                        i += 1;
                    }
                } else {
                    ltr.push(word[i]);
                    i += 1;
                }
            }
        }
    }
    return ltr;
}

function translatethis(text) {
    let trslt;
    if (text.includes(',')) {
        trslt = translate(text.replace(',', '')) + [','];
    } else if (text.includes('.')) {
        trslt = translate(text.replace(',', '')) + ['.'];
    } else {
        trslt = translate(text);
    }
    return trslt;
}

function dotranslate(word) {
    let trslt = [];
    for (let wrds of word.split(' ')) {
        if (wrds.includes('-')) {
            for (let wrd of wrds.split('-')) {
                trslt = trslt.concat(translatethis(wrd.toLowerCase()));
            }
        } else {
            trslt = trslt.concat(translatethis(wrds.toLowerCase()));
        }
    }
    return trslt;
}

function dotransliterate(word) {
    let litr = '';
    if (word.includes('.')) {
        for (let ijk = 0; ijk < word.split('.').length; ijk++) {
            let wrd = word.split('.')[ijk];
            if (wrd.includes(',')) {
                for (let idx = 0; idx < wrd.split(',').length; idx++) {
                    let wr = wrd.split(',')[idx];
                    let ltr = dotranslate(wr);
                    let isend = false;
                    for (let index = 0; index < ltr.length; index++) {
                        if (index === ltr.length - 1) {
                            isend = true;
                            let nxt = null;
                        } else {
                            nxt = ltr[index + 1];
                        }
                        let prv = index - 1 >= 0 ? ltr[index - 1] : null;

                        litr += transliterate(ltr[index], isend, prv, nxt);
                    }
                    if (idx < wrd.split(',').length - 1) {
                        litr += HURUF[','];
                    }
                }
            } else {
                let ltr = dotranslate(wrd);
                let isend = false;
                for (let index = 0; index < ltr.length; index++) {
                    if (index === ltr.length - 1) {
                        isend = true;
                        let nxt = null;
                    } else {
                        nxt = ltr[index + 1];
                    }
                    let prv = index - 1 >= 0 ? ltr[index - 1] : null;

                    litr += transliterate(ltr[index], isend, prv, nxt);
                }
                if (ijk < word.split('.').length - 1) {
                    litr += HURUF['.'];
                }
            }
        }
    } else {
        let ltr = dotranslate(word);
        let isend = false;
        for (let index = 0; index < ltr.length; index++) {
            if (index === ltr.length - 1) {
                isend = true;
                let nxt = null;
            } else {
                nxt = ltr[index + 1];
            }
            let prv = index - 1 >= 0 ? ltr[index - 1] : null;

            litr += transliterate(ltr[index], isend, prv, nxt);
        }
    }
    //console.log(litr);
    return litr;
}


function kata() {
    banner();
    Moderibetkkk();
    rl.question(`${warna.biru}(> ${warna.reset}`, (question) => {
        if (question !== 'quit') {
            try {
                console.log(warna.hijau + dotransliterate(question).toLowerCase() + warna.reset);
                console.log('\n');
            } catch (e) {
                process.exit(1);
            }
            kata();
        } else {
            rl.close();
        }
    });
}
//ModeSimple
//banner();
//console.log(`${warna.garisBawah}Masukan Kata Atau Kalimat :\n`);
kata();

```

`For more Detail` on my github repo [Aksara-Jawa](https://github.com/caturmahdialfurqon/Aksara-Jawa)

## [◉°] ScreenShot

![javanese](assets/img/Post/Javanese/Screenshot 2024-10-26 at 16.18.03.png){: w="700" h="680" }