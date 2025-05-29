---
title: How to install Chocolatey on Windows
image: scratch.png
tags:
- Tutorial
- Windows
- Powershell
---
Here's how to install Chocolatey on Windows:

1. Open PowerShell as Administrator

2. Run this command:
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

3. Verify installation by running:
```powershell
choco --version
```

You can now install packages using `choco install <package-name>`. Need elevation (admin rights) for installations.