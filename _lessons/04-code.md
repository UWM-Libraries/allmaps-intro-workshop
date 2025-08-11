---
layout: lesson
title: "Lesson 4: Coding Examples"
position: 4
permalink: /lessons/code/
---

# Environment Setup

```bash
sudo apt update && sudo apt upgrade -y

# Basic developer tools (optional)
sudo apt install -y build-essential curl git nano

# Install Node.js 20 using NodeSource
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# GDAL (geospatial library)
sudo apt install -y gdal-bin libgdal-dev

# Python tools (optional)
sudo apt install -y python3-pip python3-venv
```

## Install Allmaps CLI

```bash
npm install -g @allmaps/cli
```

Test it with

```bash
allmaps --help
```

## Optional Utilities

For clipboard interaction and working with IIIF or bash scripts:

```bash
sudo apt install -y xclip jq moreutils
```

Optionally install [`dezoomify-rs`](https://github.com/lovasoa/dezoomify-rs) for full image extraction;
This requires Rust.

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo install dezoomify-rs
```
