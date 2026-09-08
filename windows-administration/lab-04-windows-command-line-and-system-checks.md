# Lab 04 — Windows Command Line and System Checks

## Objective

Practise using Command Prompt and PowerShell to inspect system information, manage processes, check services and verify Windows system file integrity.

## Environment

- Windows 11 virtual machine
- Windows Command Prompt
- Windows PowerShell

## System Information

I practised using `hostname` and `systeminfo` to identify the computer and inspect its Windows configuration.

```cmd
hostname
systeminfo
```

I also used PowerShell to display selected system information:

```powershell
Get-ComputerInfo | Select-Object CsName, WindowsProductName, OsBuildNumber, CsTotalPhysicalMemory
```

This demonstrated how `Select-Object` limits the output to useful fields.

## Viewing and Stopping Processes

I used `tasklist` to inspect running processes and filtered the results for Notepad:

```cmd
tasklist /FI "IMAGENAME eq notepad.exe"
```

Initially, Notepad did not appear. I opened it again and repeated the check.

I then used `taskkill` to terminate Notepad, practising how to identify and stop a process.

In PowerShell, I checked the process using:

```powershell
Get-Process -Name notepad
```

## Troubleshooting Command Prompt and PowerShell

When I first attempted to run `Get-Process`, I received a “not recognised as an internal or external command” error.

The command was being entered in Command Prompt. I switched to PowerShell and successfully ran it.

This demonstrated that PowerShell cmdlets must be run in the appropriate shell.

## Checking Windows Services

I checked Print Spooler using:

```powershell
Get-Service -Name Spooler
```

The service status was **Running**.

This connected command-line service checks with my earlier practice using `services.msc`.

## Checking System File Integrity

I attempted to run:

```powershell
sfc /scannow
```

Windows initially reported that administrator privileges were required, even though I was using an administrator account.

I opened an elevated PowerShell window and ran the command successfully.

The scan completed with:

> Windows Resource Protection did not find any integrity violations.

This meant SFC found no integrity problems in the protected Windows system files it checked.

## Understanding DISM

I reviewed the purpose of DISM and how it differs from SFC:

- **SFC** checks and repairs protected Windows system files.
- **DISM** can check and repair the Windows component store used as a repair source.

Commands reviewed:

```powershell
DISM /Online /Cleanup-Image /CheckHealth
DISM /Online /Cleanup-Image /ScanHealth
DISM /Online /Cleanup-Image /RestoreHealth
```

These DISM commands were discussed but were not run during this exercise.

## What I Learned

- How to inspect system information using Command Prompt and PowerShell.
- How to identify and terminate a test process.
- How to check a Windows service from PowerShell.
- Why Command Prompt does not recognise PowerShell cmdlets.
- Why administrator group membership does not automatically elevate a terminal.
- How to run SFC and interpret a clean result.
- How DISM and SFC serve different roles in troubleshooting Windows corruption.

I also learned that effective troubleshooting depends on choosing the right tool and understanding its output, rather than memorising every command.

**Skills demonstrated:** Windows administration, Command Prompt, PowerShell, process management, service checks, UAC troubleshooting and system integrity checks.
