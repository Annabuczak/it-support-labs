# Windows Administration

Practical Windows administration labs, system configuration, maintenance, and support procedures.

## Lab 01 - Local User Account Administration

### Objective

Set up a Windows 11 virtual machine as a safe environment for practising common Windows administration and first-line IT support tasks.

### Environment

- Windows 11 virtual machine running in Oracle VirtualBox
- Anna.Admin - local IT administrator
- John.Office - standard office user
- Louie.Finance - standard finance user
- bucza - original setup/backup administrator account

### Tasks Completed

- Created separate local Windows accounts for administrator and standard users.
- Configured Anna.Admin as a member of the local Administrators group.
- Verified local administrator membership from the command line.
- Used User Account Control (UAC) and elevated administrative tools.
- Reset a standard user's password.
- Disabled and re-enabled a local user account.
- Tested logging in with different Windows user profiles.
- Troubleshot "System Error 5 - Access is denied".
- Identified that Anna.Admin initially existed as a local account but had not actually been added to the Administrators group.
- Corrected the group membership using an elevated administrator session.
- Verified the corrected administrator configuration using `net session`.

### Commands Used

```cmd
whoami
net user
net localgroup Administrators
net localgroup Administrators "Anna.Admin" /add
net session
```

### Troubleshooting - System Error 5

During the lab I repeatedly received:

```text
System error 5 has occurred.
Access is denied.
```

I confirmed which account was logged in using `whoami` and checked the local accounts using `net user`. I then inspected the actual members of the local Administrators group:

```cmd
net localgroup Administrators
```

This showed that Anna.Admin existed but was not a member of Administrators. Using the original administrator account, I opened an elevated Command Prompt and added Anna.Admin:

```cmd
net localgroup Administrators "Anna.Admin" /add
```

After signing out and back into Anna.Admin, I opened Command Prompt using **Run as administrator** and verified elevation:

```cmd
net session
```

The command completed successfully.

### What I Learned

This lab helped me understand the difference between a Windows user account, membership of the local Administrators group, and an elevated process.

Simply creating an account called `Anna.Admin` does not give it administrator privileges. The account must actually belong to the Administrators group.

I also learned that even when logged into an administrator account, Windows applications normally run without elevated privileges because of UAC. Administrative tools therefore need to be explicitly elevated when performing protected system changes.

The troubleshooting process reinforced the importance of checking the actual system state rather than assuming permissions based on an account name.

### Next Steps

- Create Office and Finance security groups.
- Configure departmental folders.
- Practise NTFS permissions and least privilege.
- Generate and troubleshoot access-denied support tickets.
- Investigate failed logons and account events using Event Viewer.
- Practise Windows administration using PowerShell.
