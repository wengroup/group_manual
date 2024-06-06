(label:laptop)=

# Setting up Mac

This page describes the basic steps to set up your Mac for computational research.

## Installing a terminal app

A fair amount of our work needs to be performed using command line (CLI) tools in a terminal. You may want to install a more powerful and easy-to-use terminal than the macOS default Terminal App.

[iTerm2](https://iterm2.com) is a great alternative. Follow the instructions on its website to download and install it.

## Setting up developer environment

Open iTerm2 and type the below command (without `$`) to set up your macOS CLI developer environment.

```
$ xcode-select --install
```

## Installing homebrew

[Homebrew](https://brew.sh) is a package manager that simplifies the installation of other software (mostly CLI tools and libraries) on macOS. To install, do

```
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installation, you can use the `brew` command to install other packages, e.g.,

```
$ brew install wget
```

See this [tutorial](https://flaviocopes.com/homebrew/) for a practical guide to Homebrew.

## Other Apps

- [PyCharm](https://www.jetbrains.com/pycharm/) - an IDE for developing python-intensive projects
- [VSCode](https://code.visualstudio.com) - a general-purpose IDE
- [VPN](https://uh.edu/infotech/services/computing/networks/vpn/) - getting access to UH resources (e.g. library and HPE DSI clusters) from your internet connection when off campus

## Optional

- [Zotero](https://www.zotero.org) - a reference manager
- [Obsidan](https://obsidian.md) - a markdown-based notetaking app
- [Ovito](https://www.ovito.org) - an atomic structure viewer and data analysis tool
- [Studio 3T](https://studio3t.com) - a GUI for MongoDB
