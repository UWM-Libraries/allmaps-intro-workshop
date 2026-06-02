---
layout: lesson
title: "Lesson 4: Command Line Setup"
position: 4
permalink: /lessons/command-line-setup/
---

# Lesson 4: Command Line Setup

The next lessons use command-line tools to work with Allmaps annotations, IIIF images, GeoTIFFs, GeoJSON, and small web mapping examples.

If you already have a Unix-like terminal with Node.js, npm, GDAL, Allmaps CLI, `jq`, and `dezoomify-rs`, you can skim this page and continue to [Lesson 5: Exporting a GeoTIFF with Allmaps CLI]({{ '/lessons/geotiff-export/' | relative_url }}).

> **Warning:**
>
> This lesson assumes some familiarity with the command line in a Unix environment
> (Linux, macOS, or a Unix-like environment on a Windows PC),
> installing packages, and generating and running scripts from the command line.
>
> Never copy and paste code into your terminal unless you understand what it is doing.
> Installation and compatibility will vary depending on your operating system,
> OS version, and shell environment.
>
{: .callout .warning }

## Required Tools

For the advanced workshop lessons, you will need:

- [Node.js](https://nodejs.org/en/download) and `npm`
- [Allmaps Command Line](https://www.npmjs.com/package/@allmaps/cli)
- [GDAL](https://gdal.org/en/stable/download.html)
- `jq`
- [dezoomify-rs](https://github.com/lovasoa/dezoomify-rs)

## Windows Only: Set up WSL

macOS and Linux users can skip this section and jump to [Linux and Unix](#linux-and-unix).

This lesson uses WSL for Windows because the command-line tools in this section are easiest to install and teach in a Unix-like environment.
WSL gives Windows users a Linux shell that behaves much like the macOS and Linux workflows used in the rest of the lesson, which keeps commands, paths, and troubleshooting more consistent.
Native Windows workflows are possible, but they require different setup steps.

For more detailed setup instructions, see Microsoft's [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install) documentation.

Open PowerShell as an administrator and install WSL:

```powershell
wsl --install
```

This installs Ubuntu by default. If WSL is already installed but Ubuntu is not, you can install Ubuntu explicitly:

```powershell
wsl --install -d Ubuntu
```

Open Ubuntu from the Windows Start menu. When the Ubuntu prompt appears, continue with the Linux and Unix instructions below.

## Linux and Unix

The commands below are written for Ubuntu and Debian-based environments, including Ubuntu on WSL, that use the `apt` package manager.
Other Linux or Unix-like systems may use different package managers, package names, and compilation methods.

Refresh the package list and apply available system updates before installing new tools:

```bash
sudo apt update
sudo apt upgrade
```

Install the current long-term support (LTS) version of Node.js using the standard installer or package manager for your operating system.

On Ubuntu, Debian, or Ubuntu on WSL, you can use the instructions from Node.js:

[https://nodejs.org/en/download](https://nodejs.org/en/download)

Use Node.js 22 or newer, preferably the current LTS version.

After installation, confirm that Node.js and npm are available:

```bash
node --version
npm --version
```

Install GDAL and `jq`:

```bash
sudo apt install -y gdal-bin libgdal-dev jq
```

## macOS

Install [Homebrew](https://brew.sh/) if not already installed.

Refresh Homebrew's package list:

```zsh
brew update
```

Install Node.js, GDAL, and `jq`:

```zsh
brew install node gdal jq
```

After installation, confirm that Node.js and npm are available:

```bash
node --version
npm --version
```

## Install Allmaps CLI

Install the Allmaps CLI:

```bash
npm install -g @allmaps/cli
```

Confirm that Allmaps CLI and GDAL are available:

```bash
allmaps --help
gdalinfo --version
jq --version
```

## Install dezoomify-rs

`dezoomify-rs` is used for full image extraction when a IIIF server does not provide the full-resolution image directly through Allmaps CLI.

On Ubuntu/Debian or Ubuntu on WSL, install Rust and then install `dezoomify-rs` with Cargo:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Load Cargo in your current terminal session:

```bash
source "$HOME/.cargo/env"
```

Confirm Cargo is available:

```bash
cargo --version
```

Install `dezoomify-rs`:

```bash
cargo install dezoomify-rs
```

On macOS, install `dezoomify-rs` with Homebrew instead:

```zsh
brew install dezoomify-rs
```

Confirm the tool is available:

```bash
dezoomify-rs --help
```

> **Warning:**
>
> If installation fails, the most likely missing pieces are Node.js, npm, GDAL, Rust/Cargo, or small command-line utilities such as `jq`.
> After installing a new tool, you may need to restart your terminal before the command is available.
>
{: .callout .warning }

When these tools are installed, continue to [Lesson 5: Exporting a GeoTIFF with Allmaps CLI]({{ '/lessons/geotiff-export/' | relative_url }}).
