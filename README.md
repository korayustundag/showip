# ShowIP

<p align="center">
Portable IPv4 detection tool for Unix-like systems
</p>

<p align="center">

![License](https://img.shields.io/badge/license-BSD--2--Clause-blue)
![POSIX](https://img.shields.io/badge/POSIX-Compatible-green)
![Shell](https://img.shields.io/badge/Shell-POSIX-lightgrey)
![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20BSD%20%7C%20macOS-blue)

</p>

---

## Overview

**ShowIP** is a lightweight, portable, and POSIX-compliant shell tool that detects your **public** and **local IPv4 addresses**.

It is designed to work across multiple Unix-like systems including **Linux**, **BSD**, and **macOS**, while keeping dependencies minimal.

The script automatically detects available networking utilities (`curl`, `wget`, or `fetch`) and uses multiple IP services as **failover providers** to ensure reliable results.

ShowIP is particularly useful for:

* shell scripts
* automation workflows
* system diagnostics
* DevOps tooling
* CI/CD environments

---

## Features

* Detect **Public IPv4**
* Detect **Local IPv4**
* **Automatic failover** between multiple IP providers
* **POSIX compliant shell script**
* **Extremely lightweight**
* **Zero external dependencies required**
* Works on **Linux, BSD, and macOS**
* Optional **JSON output** for scripting
* VM / container safe local IP detection

---

## Table of Contents

* [Overview](#overview)
* [Features](#features)
* [Installation](#installation)
* [Usage](#usage)
* [Examples](#examples)
* [Output Formats](#output-formats)
* [How It Works](#how-it-works)
* [Portability](#portability)
* [Dependencies](#dependencies)
* [Security Considerations](#security-considerations)
* [Contributing](#contributing)
* [License](#license)

---

# Installation

## Clone the repository

```bash
git clone https://github.com/korayustundag/showip.git
cd showip
chmod +x showip
```

---

## Install globally (recommended)

```bash
sudo install -m 755 showip /usr/local/bin/showip
```

Now you can run it anywhere:

```bash
showip
```

---

## Download manually

```bash
curl -O https://raw.githubusercontent.com/korayustundag/showip/main/showip
chmod +x showip
```

---

# Usage

```bash
showip [options]
```

### Options

| Option | Description         |
| ------ | ------------------- |
| `-l`   | Show only local IP  |
| `-p`   | Show only public IP |
| `-j`   | JSON output         |
| `-h`   | Display help        |

---

# Examples

## Show both public and local IP

```bash
showip
```

Example output:

```
Public IPv4 : 13.107.213.60
Local  IPv4 : 192.168.1.24
```

---

## Show only public IP

```bash
showip -p
```

Example:

```
Public IPv4 : 13.107.213.60
```

---

## Show only local IP

```bash
showip -l
```

Example:

```
Local  IPv4 : 192.168.1.24
```

---

## JSON output

```bash
showip -j
```

Example:

```json
{
  "public_ipv4": "13.107.213.60",
  "local_ipv4": "192.168.1.24"
}
```

This is useful for:

* shell scripting
* monitoring tools
* automation pipelines

---

# Output Formats

### Human readable

```
Public IPv4 : 13.107.213.60
Local  IPv4 : 192.168.1.24
```

### JSON

```json
{
  "public_ipv4": "13.107.213.60",
  "local_ipv4": "192.168.1.24"
}
```

---

# How It Works

## Public IP Detection

ShowIP queries several IP detection services sequentially:

* https://icanhazip.com
* https://api.ipify.org
* https://whatismyip.akamai.com
* https://checkip.amazonaws.com
* https://ipinfo.io/ip

If one service fails or times out, the script **automatically falls back to the next provider**.

---

## Local IP Detection

Instead of parsing raw `ifconfig` output (which is unreliable across platforms), ShowIP determines the active interface using routing information.

### Linux

Uses:

```
ip route get <target>
```

### BSD / macOS

Uses:

```
route -n get <target>
ifconfig
```

This routing-based detection is more reliable and works properly inside:

* Virtual Machines
* Containers
* NAT environments

---

# Portability

ShowIP is designed to be **fully portable** across Unix-like systems.

Supported platforms:

* Linux
* FreeBSD
* OpenBSD
* NetBSD
* macOS

The script is written using **POSIX shell**, avoiding Bash-specific features.

---

# Dependencies

ShowIP automatically detects one of the following tools:

| Tool  | Purpose                     |
| ----- | --------------------------- |
| curl  | HTTP requests               |
| wget  | HTTP requests               |
| fetch | HTTP requests (BSD systems) |

Only **one of these tools** is required.

---

# Security Considerations

* Only trusted public IP detection services are used.
* HTTP requests are performed with timeouts to avoid hanging processes.
* Output is validated to ensure valid IPv4 addresses.
* No sensitive information is stored or transmitted.

---

# Contributing

Contributions are welcome.

You can contribute by:

* reporting bugs
* suggesting improvements
* submitting pull requests
* improving documentation

Please open an **Issue** before submitting major changes.

---

# License

This project is licensed under the **BSD 2-Clause License**.

See the `LICENSE` file for details.

---

# Author

**Koray Üstündağ**

---

# Support

If you find this project useful, consider:

⭐ Starring the repository
🐛 Reporting issues
🔧 Contributing improvements
