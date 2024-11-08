---
layout: post
title: "How To Setup Your Mac Terminal"
date: 2024-05-25 18:18:15 +07:00
categories: [HOW TO,Tips]
tags: [Tips&Trick]
description: Customize Your Mac Terminal (Iterm2) with ZSH
image: /assets/img/Post/How-To-Setup-Your-Mac-Terminal/terminal.jpeg
alt: "image alt text"
comments: true
---

## How To Setup Your Mac Terminal
> Let's starting....
{: .prompt-tip }

### - Install Homebrew
- [x] First thing you need is installing Homebrew, you can skip this if you're already installed Homebrew.

Open up a terminal window and install homebrew with the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### - Add Homebrew To Path

> After installing, add it to the path.
(replace `[username]`) with your actual username.
{: .prompt-warning }

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> /Users/[username]/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

### - Install iTerm2

Switch to iTerm2 for the remainder of this walkthrough.

### - Install Git

If you don’t have it installed, install git as well use homebrew to install it.

```bash
brew install git
```

### - Install Oh My Zsh

Now you need to install Oh my Zsh.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### - Install PowerLevel10K Theme for Oh My Zsh

Run this to install PowerLevel10K.

```bash
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```
Now that it’s installed, open the ”~/.zshrc” file with your preferred editor and change the value of “ZSH_THEME” as shown below.

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```
> To reflect this change on your terminal, restart it or run this command below.
{: .prompt-tip }
```bash
source ~/.zshrc
```
### - Install Meslo Nerd Font

Install the font by pressing “y” and then quit iTerm2.

### - Update VSCode Terminal Font
> `(Optional)`
{: .prompt-info }
Open settings.json and add this line.

```bash
"terminal.integrated.fontFamily": "MesloLGS NF"
```

### - Configure PowerLevel10K

> Restart iTerm2.
{: .prompt-tip }
You should now be seeing the PowerLevel10K configuration process. If you don’t, run the following.

```bash
p10k configure
```
Follow the instructions for the PowerLevel10K configuration to make your terminal look as desired.

### - Increase Terminal Font Size

- [x] Open iTerm2 preferences
- [x] Go to Profiles > Text
- [x] Increase my font size to about 20px

### - Change iTerm2 Colors to My Custom Theme

- [x] Open iTerm2
- [x] Download my color profile by running the following command (will be added to Downloads folder).

```bash
curl https://raw.githubusercontent.com/josean-dev/dev-environment-files/main/coolnight.itermcolors --output ~/Downloads/coolnight.itermcolors
```
- [x] Open iTerm2 preferences.
- [x] Go to Profiles > Colors.
- [x] Import the downloaded color profile (coolnight).
- [x] Select the color profile (coolnight).

You can find other themes here the link: [Iterm2 Color Schemes](https://iterm2colorschemes.com/)

### - Install ZSH Plugins

Install zsh-syntax-highlighting.
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
Open the ”~/.zshrc” file in your desired editor and modify the plugins line to what you see below.

```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting web-search)
```
Load these new plugins by running.

```bash
source ~/.zshrc
```

### - You’re Done!
![Furqonic](/assets/img/Post/How-To-Setup-Your-Mac-Terminal/ss1.png)

> `With that, you’re finished and should have a much better terminal experience! :')`
