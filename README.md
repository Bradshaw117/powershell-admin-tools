# PowerShell Admin Tools

## Overview
This project contains beginner PowerShell administrative tools created as part of my IT and systems administration learning path.

The scripts focus on system information gathering, automation, and troubleshooting tasks commonly used in help desk and IT support environments.

---

## Technologies Used
- PowerShell
- Windows 11
- Visual Studio Code

---

## Scripts Included
# ==========================================
# System Information Report Script
# Author: Kevin Bradshaw
# ==========================================

Write-Host "Gathering system information..." -ForegroundColor Green

# Computer Name
$computerName = $env:COMPUTERNAME

# Operating System
$os = Get-CimInstance Win32_OperatingSystem

# CPU Information
$cpu = Get-CimInstance Win32_Processor

# RAM Information
$ram = Get-CimInstance Win32_PhysicalMemory

# Disk Information
$disk = Get-CimInstance Win32_LogicalDisk -Filter "DriveType=3"

# Network Information
$network = Get-NetIPAddress -AddressFamily IPv4 |
Where-Object {
    $_.IPAddress -notlike "127.*" -and
    $_.IPAddress -notlike "169.254*"
}

Write-Host "`n===== SYSTEM REPORT =====" -ForegroundColor Cyan

Write-Host "`nComputer Name:"
Write-Host $computerName

Write-Host "`nOperating System:"
Write-Host $os.Caption

Write-Host "`nCPU:"
Write-Host $cpu.Name

Write-Host "`nInstalled RAM:"
$totalRAM = ($ram.Capacity | Measure-Object -Sum).Sum / 1GB
Write-Host ("{0:N2} GB" -f $totalRAM)

Write-Host "`nDisk Drives:"
foreach ($d in $disk) {
    Write-Host "$($d.DeviceID) - Free Space: $([math]::Round($d.FreeSpace / 1GB,2)) GB"
}

Write-Host "`nIPv4 Addresses:"
foreach ($ip in $network) {
    Write-Host $ip.IPAddress
}

Write-Host "`nSystem report complete." -ForegroundColor Green

### System Information Report
Collects:
- Computer name
- Operating system
- CPU information
- Installed RAM
- Disk space
- Network IP addresses

---

## Skills Demonstrated
- PowerShell scripting
- Windows administration
- System diagnostics
- Command-line tools
- Documentation

---

## Screenshots
<img width="1920" height="1080" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/33e9713a-1d6b-46cc-b01d-e050834b011a" />
<img width="1920" height="1080" alt="Screenshot (1)" src="https://github.com/user-attachments/assets/5f1fc00e-5c69-4088-8d28-35b8126151da" />


---

## Lessons Learned
This project helped reinforce:
- basic PowerShell syntax
- Windows system management
- administrative scripting workflows
- troubleshooting execution policies
