---
title: Python Obfuscate Emojis
date: 2024-10-25 22:00:30 +07:00
description: Obfuscate Your Python Source Code with Emojis or Emoticons 😬 🤯 😂.
image : assets/img/Post/Python.jpeg
author: "cmalf"
---

# 🐍 Obfuscate Your Python Source Code with Emojy 😬 🤯  😬 🤫  🤣 😂

Emojis and emoticons will be used in this script to obfuscate your Python source code. However, please note that I cannot guarantee the security of your source code once this process is complete. 

## `Source` CODE

```python
#!/usr/bin/env python3
# -*- coding: UTF-8 -*-

from pprint import pformat
from termcolor import colored
import os

EMOTICONS = [":)", ":D", ":P", ":S", ":(", "=)", "=/", ":/", ":{", ";)"]
EMOJIS = [
    "\U0001f600",
    "\U0001f603",
    "\U0001f604",
    "\U0001f601",
    "\U0001f605",
    "\U0001f923",
    "\U0001f602",
    "\U0001f609",
    "\U0001f60A",
    "\U0001f61b",
]
MAX_STR_LEN = 70

def banner():
    print("╭━━━╮╱╱╱╱╱╱╱╱╱╱╱╱╱╭━━━┳╮Python 3.13")
    print("┃╭━━╯╱╱╱╱╱╱╱╱╱╱╱╱╱┃╭━━┫┃Obfuscator ")
    print(colored("┃╰━━┳╮╭┳━┳━━┳━━┳━╮┃╰━━┫┃╭╮╱╭┳━╮╭━╮XD", 'green'))
    print(colored("┃╭━━┫┃┃┃╭┫╭╮┃╭╮┃╭╮┫╭━━┫┃┃┃╱┃┃╭╮┫╭╮╮🤫", 'green'))
    print(colored("┃┃╱╱┃╰╯┃┃┃╰╯┃╰╯┃┃┃┃┃╱╱┃╰┫╰━╯┃┃┃┃┃┃┃🤯", 'green'))
    print(colored("╰╯╱╱╰━━┻╯╰━╮┣━━┻╯╰┻╯╱╱╰━┻━╮╭┻╯╰┻╯╰╯:D", 'green'))
    print("╱╱╱╱╱╱╱╱╱╱╱┃┃╱╱╱╱╱╱╱╱╱╱╱╭━╯┃Emoticons")
    print("╱╱╱╱╱╱╱╱╱╱╱╰╯╱╱╱╱╱╱╱╱╱╱╱╰━━╯Emojis")

def chunk_string(in_s, n):
    return "\n".join(
        "{}\\".format(in_s[i : i + n]) for i in range(0, len(in_s), n)
    ).rstrip("\\")

def encode_string(in_s, alphabet):
    d1 = dict(enumerate(alphabet))
    d2 = {v: k for k, v in d1.items()}
    return (
        'exec("".join(map(chr,[int("".join(str({}[i]) for i in x.split())) for x in\n'
        '"{}"\n.split("  ")])))\n'.format(
            pformat(d2),
            chunk_string(
                "  ".join(" ".join(d1[int(i)] for i in str(ord(c))) for c in in_s),
                MAX_STR_LEN,
            ),
        )
    )

def main():
    banner()
    while True:
        print(colored("\nMenu:", 'yellow'))
        print("1. Obfuscate Emoticons :D ")
        print("2. Obfuscate Emojis 🤣")
        print(colored("3. About This Tools", 'green'))
        print(colored("4. Exit", 'red'))
        choice = input("Select an option: ")

        if choice == '1':
            in_file = input(colored("Enter input file name: ", 'blue'))
            out_file = input(colored("Enter output file name: ", 'blue'))
            with open(in_file) as in_f, open(out_file, "w") as out_f:
                out_f.write(encode_string(in_f.read(), EMOTICONS))
            print(colored("Obfuscation done with Emoticons.", 'green'))
        
        elif choice == '2':
            in_file = input(colored("Enter input file name: ", 'blue'))
            out_file = input(colored("Enter output file name: ", 'blue'))
            with open(in_file) as in_f, open(out_file, "w") as out_f:
                out_f.write(encode_string(in_f.read(), EMOJIS))
            print(colored("Obfuscation done with Emojis.", 'green'))
        
        elif choice == '3':
            print(colored("Desc: This program obfuscates Python scripts using emoticons or emojis.", 'yellow'))
        
        elif choice == '4':
            print(colored("Exiting...", 'red'))
            break
        
        else:
            print(colored("Invalid option. Please try again.", 'red'))

        cont = input(colored("Do you want to continue? (y/n): ", 'yellow')).lower()
        if cont == 'y':
            os.system('clear' if os.name == 'posix' else 'cls')
            banner()
        else:
            print(colored("Exiting...", 'red'))
            break

if __name__ == "__main__":
    main()

```

`For more Detail` on my github repo [Python Obfuscate Emoji](https://github.com/caturmahdialfurqon/Python-Obfuscator-Emojis)

## [◉°] ScreenShot (gif)

![pythonobfuscate](assets/img/Post/Python-obfuscate/CleanShot 2024-10-26 at 08.51.15.gif){: w="700" h="680" }