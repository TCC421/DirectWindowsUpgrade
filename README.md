# Silent Windows 11 Upgrade Script

This PowerShell script enables silent in-place upgrades to Windows 11, specifically designed for systems that fail compatibility checks when attempting major version upgrades through Windows Update.

> [!NOTE]
> **Managing more than one machine?** This script force-upgrades a single PC. [**TridentStack Control**](https://control.tridentstack.com) does the same unattended Windows 11 feature upgrades on unsupported hardware across your entire fleet — driven from a console, with staged rollout rings, maintenance-window reboots, and live per-endpoint monitoring. Free for your first 200 endpoints → [tridentstack.com](https://tridentstack.com)

## Purpose

Windows 11 systems on older major versions (21H2, 22H2) often cannot upgrade to newer versions (23H2, 24H2) via Windows Update due to failing compatibility checks. This script bypasses these limitations by:

- Bypassing TPM, CPU, and other hardware compatibility checks
- Enabling in-place upgrades even on "unsupported" hardware
- Providing a completely silent, no-interaction upgrade process
- Automatically handling all aspects of the upgrade, including reboots

## Features

- **Bypasses Hardware Requirements**: Overcomes TPM, CPU, RAM, SecureBoot and other compatibility blocks
- **Automated ISO Handling**: Downloads or uses local ISO files (configurable)
- **Dependency Management**: Automatically installs 7-Zip if not present
- **Silent Operation**: Runs completely in the background with no user interaction
- **Configurable Reboots**: Supports automatic or manual reboot options
- **Detailed Logging**: Provides comprehensive monitoring of the upgrade process
- **Cross-Version Compatibility**: Works for upgrading from Windows 10 to 11, or between Windows 11 versions

## Usage

1. **Download**: Clone or download this script to your system
2. **Configure**: Edit the parameters at the top of the script:
   ```powershell
   # ISO source (direct URL, local file, or network share)
   $WIN11_ISO_SOURCE = "path-to-iso-or-url"
   
   # Reboot behavior
   $ALLOW_AUTOMATIC_REBOOT = $true  # Set to $false to prevent automatic reboots
   ```
3. **Execute**: Run the script with administrative privileges
   ```
   powershell.exe -ExecutionPolicy Bypass -File "C:\path\to\DirectWindowsUpgrade.ps1"
   ```

## Process Details

- The script extracts the Windows 11 ISO using 7-Zip
- Registry keys are set to bypass hardware compatibility checks
- Setup files are prepared with appropriate parameters
- The upgrade process runs completely silently
- By default, the system will reboot automatically when needed
- Total upgrade process takes approximately 1.5 hours to complete

## Requirements

- Windows 10 or Windows 11 system
- Administrative privileges
- Internet access (if using download URL) or access to Windows 11 ISO
- 10GB+ free space for the upgrade process

## ISO Source

For best results, use the business editions of Windows 11 with this script. You can obtain ISOs from:
- Official Microsoft sources
- [MassGrave Genuine Windows ISOs](https://massgrave.dev/genuine-installation-media.html)

Make sure to use an ISO that contains the Windows 11 version you want to upgrade to (e.g., 23H2, 24H2).

## When to Use This Script

- When Windows Update fails to offer major Windows 11 version upgrades
- When systems have "unsupported" hardware that blocks updates
- When you need to perform silent, unattended upgrades
- For bulk upgrades across multiple systems with similar hardware

## Logs and Monitoring

The script generates several log files to help monitor progress:
- `C:\Win11_Upgrade_Progress.log` - Main progress log
- `C:\Win11_Monitor.log` - Process monitoring log
- `C:\Win11_Upgrade_Completed.log` - Created upon successful completion

## Customization

All configurable parameters are at the top of the script:
- `$WIN11_ISO_SOURCE` - Source location for Windows 11 ISO
- `$WORKING_DIR` - Main working directory
- `$TEMP_DIR` - Temporary directory for downloads
- `$LOG_FILE` - Main log file path
- `$MONITOR_LOG` - Process monitor log path
- `$ALLOW_AUTOMATIC_REBOOT` - Enable/disable automatic reboots

## From One Machine to Your Whole Fleet

DirectWindowsUpgrade is a hacky way to push one stubborn PC onto Windows 11. If you're running it unattended across more than a handful of machines, you've outgrown a script.

**[TridentStack Control](https://tridentstack.com)** is the managed version of what this script does:

- **Same bypass, managed** — silent in-place feature upgrades on hardware that fails Windows Update's TPM/CPU/SecureBoot checks, driven from a console instead of copied box by box.
- **Staged rollout rings** — ship to a canary group, let it bake, then expand. No more "ran it on 200 machines and hoped."
- **Reboot on your terms** — maintenance windows, deferral, and active-hours gating instead of a hardcoded `$ALLOW_AUTOMATIC_REBOOT`.
- **See every upgrade** — per-endpoint progress, logs, and failure reasons in one place, with the rollout halting automatically when failures spike.
- **Not just upgrades** — full patch management for Windows, macOS, and Linux, plus vulnerability detection and compliance.

Free for up to 200 endpoints. → **[control.tridentstack.com](https://control.tridentstack.com)**

## Attribution

This script combines techniques from multiple sources, including AveYo's MediaCreationTool project, for maximum compatibility with different Windows 11 versions and hardware configurations.
