---
description: This page is to detail the WS client to REST Container
---

# Cheesy WS to REST Container

## Description&#x20;

The Cheesy WS to REST translator script is a PowerShell script that takes in the Cheesy Arena WS IO and translate it to a REST interface with the PODE library.  This is used in conjunction with the scorekeeping container to have a clean endpoint that the Scorekeeping container, and the AV Control Container can interact and send commands to Cheesy Arena with minimal overhead and duplicate code.



Due to the complex library based on the code from the user byt3bl33d3r PODE cannot directly interact with the async WS .NET code without breaking either library.

## Install

The Following code from Microsoft installs Powershell 7 into the Debian Container.  Note that the package file address will need to be updated when Powershell does get updated.

```sh
###################################
# Prerequisites

# Update the list of packages
apt-get update

# Install pre-requisite packages.
apt-get install -y wget

# Download the PowerShell package file
wget https://github.com/PowerShell/PowerShell/releases/download/v7.4.6/powershell_7.4.6-1.deb_amd64.deb

###################################
# Install the PowerShell package
dpkg -i powershell_7.4.6-1.deb_amd64.deb

# Resolve missing dependencies and finish the install (if necessary)
apt-get install -f

# Delete the downloaded package file
rm powershell_7.4.6-1.deb_amd64.deb
```
