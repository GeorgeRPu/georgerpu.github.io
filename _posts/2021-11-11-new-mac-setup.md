---
layout: post
title: "New Mac Setup 2021"
date: 2021-11-11
description: "Guide to setting up an ARM Mac for software development"
giscus_comments: true
toc:
  sidebar: left
tags: software-engineering
citation: true
---

In late 2021, I switched my personal computer from a Surface Book 2 to a new M1 Pro Macbook Pro. It has been quite an experience switching OSes. To help, I created this setup guide.

## Homebrew

The de facto MacOS package manager. I prefer to install apps via Homebrew, if possible.

Install by following the instructions at <https://brew.sh>.

## Oh My Zsh

A customizable configuration and plugin system for Zsh.

Install by following the instructions at <https://ohmyz.sh>.

### Powerlevel10k

An Oh My Zsh Theme.

Install by following the instructions at <https://github.com/romkatv/powerlevel10k#oh-my-zsh>. Use the Oh My Zsh method. Run `p10k configure` to configure the theme.

## Anaconda

A data science flavored Python installation with by far the best Python package manager.

Install by following the instructions at <https://www.anaconda.com>. The "Install for me" option creates Anaconda directory at `~/opt/anaconda3`.

### PyCharm

A Python IDE with developer and scientific tools.

To install, navigate to the Download page of <https://www.jetbrains.com/pycharm/>.

## Git

Git comes preinstalled on Macs.

### Github Desktop

The official GUI client for Github. For a more advanced GUI client see <https://fork.dev/>.

Install using Homebrew.

```bash
brew install --cask github
```

## Java

Maybe the popular programming language for individuals and enterprises.

Install using Homebrew.

```bash
brew install openjdk
```

### IntelliJ

The best Java IDE.

To install, navigate to the Download page of <https://www.jetbrains.com/idea/>.

## Julia

A scientific programming language that is as fast as C++, but as easy as Python. Note that the ARM installation for MacOS is currently Tier 3.

Install by following the instructions at <https://julialang.org>.

## Latex

The de facto LaTeX distribution for Mac is MacTeX.

Install using Homebrew.

```bash
brew install --cask mactex-no-gui
```

### Texpad

A feature laden, MacOS exclusive LaTeX editor.

Install using Homebrew.

```bash
brew install --cask texpad
```

### Texstudio

The best LaTeX editor across multiple systems.

Install using Homebrew.

```bash
brew install --cask texstudio
```

## NodeJS

A Desktop JS runtime built on Chrome's V8 engine. The current LTS version is 16.

Install using Homebrew.

```
brew install node@16
```

## Apps

### Appcleaner

An Application uninstaller that searches through the entire file system.

Install using Homebrew.

```bash
brew install --cask appcleaner
```

### Chrome

The de facto internet browser (to our benefit and detriment).

Install by following the instructions at <https://www.google.com/chrome/>.

### Discord

Gaming centric chat and voice rooms.

Install using Homebrew.

```bash
brew install --cask discord
```

### iTerm2

iTerm2 is to Terminal what Windows Terminal is to Command Prompt.

Install using Homebrew.

```bash
brew install --cask iterm2
```

### Monitor Control

Allow you to control the brightness of external monitors using the brightness keys on your keyboard or a brightness slider in the menu bar.

Install using Homebrew.

```bash
brew install --cask monitorcontrol
```

### OneDrive

A cloud file storage client. Included on Windows machines by default.

Install using Homebrew.

```bash
brew install --cask onedrive
```

### Nota

A new Markdown editor from the creators of Caret.

Install using Homebrew.

```bash
brew install --cask nota
```

### Rectangle

A window size manager for MacOS. Rectangle is free unlike Magnet.

Install using Homebrew.

```bash
brew install --cask rectangle
```

### Scroll Reverser

Allows the scroll direction to be different for mouse and trackpad.

Install using Homebrew.

```bash
brew install --cask scroll-reverser
```

### Spotify

The most popular app for streaming music and listening to podcasts

Install using Homebrew.

```bash
brew install --cask spotify
```

### Strongbox

The best Keepass client for MacOS. Strongbox also has an iOS app.

Download from the App store.

<https://strongboxsafe.com>

### Things

Todo list software preferences are person specific, but Things delivers everything I expect from a todo list in a beautiful package.

Download from the App store.

<https://culturedcode.com/things/>

### Typora

The best Markdown editor on any OS.

Install using Homebrew.

```bash
brew install --cask typora
```

### VSCode

The best text editor for programming.

Install using Homebrew.

```bash
brew install --cask visual-studio-code
```

Login to Github to sync settings and extensions. Alternatively, install the following extensions.

```bash
# general
code --install-extension visualstudioexptteam.vscodeintellicode
code --install-extension ms-vscode-remote.vscode-remote-extensionpack
code --install-extension mhutchie.git-graph
code --install-extension christian-kohler.path-intellisense
# other views
code --install-extension ms-vscode.hexeditor
# github
code --install-extension github.remotehub
code --install-extension github.copilot
# python
code --install-extension ms-python.python
code --install-extension ms-toolsai.jupyter-renderers
code --install-extension njpwerner.autodocstring
code --install-extension kevinrose.vsc-python-indent
# html + javascript + css
code --install-extension mgmcdermott.vscode-language-babel
code --install-extension dbaeumer.vscode-eslint
code --install-extension bradlc.vscode-tailwindcss
code --install-extension mikestead.dotenv
# c++
code --install-extension ms-vscode.cpptools
# markdown
code --install-extension bierner.markdown-mermaid
# theming
code --install-extension zhuangtongfa.material-theme
code --install-extension pkief.material-icon-theme
```

Follow the instructions at <https://patelhiren.com/blog/setting-vscode-as-default-text-editor-on-macos/> to make VSCode the default text editor.

### Zoom

The de facto video call/conferencing app since March 2020.

Install using Homebrew.

```bash
brew install --cask zoom
```

## Zotero

Free paper and reference manager with paid cloud storage. You should also install the Zotero Connector extension for your browser to add references to Zotero from the web.

Install using Homebrew.

```bash
brew install --cask zotero
```

## Utilities

### fzf

Fuzzy finder to look up files. fzf also overrides 3 terminal keybindings that makes it easier to lookup old commands and change directories.

Install using Homebrew.

```bash
brew install --cask fzf
```

### lsd

Colorized ls built using Rust.

Install using Homebrew.

```bash
brew install lsd
```

## Dock

From left to right: Finder, LaunchPad, Safari, Chrome, Mail, FaceTime, Messages, Mail, Maps, Photos, Calendar, Contacts, Reminders, Things, Notes, Typora, AppStore, System Preferences.

## Other Setup Guides

- [The 11 best apps for your new Mac](https://www.theverge.com/2019/12/27/21029022/best-macos-apps-apple-mac-macbook-air-pro-airmail-alfred-bear-lastpass-vlc)
- [11 great apps ready for your new 2020 M1 Mac](https://www.theverge.com/22188814/apple-apps-m1-macbook-air-pro-mac-mini-lightroom-office-2020)
- <https://sourabhbajaj.com/mac-setup/>
- <https://www.swyx.io/new-mac-setup-2021>
