## Lab 02 — NTFS Permissions and File Sharing

### Objective

The aim of this lab was to practise managing NTFS permissions, local security groups, folder inheritance and Windows file sharing. I also tested permissions using different user accounts and troubleshot access problems.

### Lab Environment

- Windows 11 virtual machine
- Oracle VirtualBox
- Computer name: BUCZAKLAB-PC02
- Administrator account: Anna.Admin
- Standard user accounts: John.Office and Louie.Finance

### Folder Structure

I created the following folders:

C:\BUCZAKLAB\Finance  
C:\BUCZAKLAB\HR  
C:\BUCZAKLAB\Operations  
C:\BUCZAKLAB\Shared

Test files were added to the folders so I could check whether different users could open and modify them.

### Local Security Groups

I created three local security groups:

- Finance-Users
- HR-Users
- Operations-Users

The users were assigned as follows:

John.Office → HR-Users  
Louie.Finance → Finance-Users and Operations-Users

This allowed permissions to be assigned to groups rather than directly to individual users.

### Configuring NTFS Permissions

I used the Security and Advanced Security settings on the folders to control access.

For restricted folders, inherited permissions were removed so that access could be controlled using the relevant security group.

Administrators and SYSTEM retained Full Control.

Department groups were then given the permissions required to work with their folders.

For example:

Finance-Users → Finance  
HR-Users → HR  
Operations-Users → Operations

I tested the permissions by signing into the different Windows accounts.

John.Office could access the HR folder but was prevented from accessing Finance.

Louie.Finance could access Finance and Operations but was prevented from accessing HR.

### Troubleshooting Access Denied

One of the main problems I encountered was that users initially had access to folders they were not supposed to access.

I investigated the permissions using:

`icacls C:\BUCZAKLAB\Finance`

and

`icacls C:\BUCZAKLAB\HR`

This showed that permissions were being inherited from the parent folder.

Entries marked `(I)` were inherited permissions.

I disabled inheritance and removed the inherited permissions before applying the correct security groups.

I then tested the folders again using the standard user accounts.

### Explicit DENY Problem

During troubleshooting I added a DENY permission for Authenticated Users.

This caused an unexpected problem because Anna.Admin is also an authenticated user, so the administrator account was affected by the DENY rule.

I removed the DENY entry and instead controlled access by only granting permissions to the groups that required them.

This demonstrated why broad DENY permissions should be used carefully.

### Useful Commands

Check the current user:

`whoami`

View group membership:

`whoami /groups`

View NTFS permissions:

`icacls C:\BUCZAKLAB\Finance`

Remove inherited permissions:

`icacls C:\BUCZAKLAB\Finance /inheritance:r`

Restore inheritance:

`icacls C:\BUCZAKLAB\Finance /inheritance:e`

### Permission Flags

During the lab I also learned how to interpret common `icacls` permission flags:

`(I)` — Inherited  
`(F)` — Full Control  
`(M)` — Modify  
`(RX)` — Read and Execute  
`(W)` — Write  
`(OI)` — Files inherit the permission  
`(CI)` — Subfolders inherit the permission

### File Sharing

I shared the following folder across the local Windows system:

`C:\BUCZAKLAB\Shared`

Using:

Properties → Sharing → Advanced Sharing

The folder was shared as:

`\\BUCZAKLAB-PC02\Shared`

This demonstrated the difference between NTFS permissions and share permissions.

NTFS permissions control access to files and folders on the filesystem, while share permissions apply when the folder is accessed through a network share.

### Mapping a Network Drive

I mapped the Shared folder as the `S:` drive using:

`\\BUCZAKLAB-PC02\Shared`

The mapped drive then appeared in File Explorer under This PC.

I also disconnected the mapped drive and successfully reconnected it to practise a common IT support task.

### Troubleshooting Lessons

This lab involved several permission problems which required troubleshooting rather than simply following a set of instructions.

The main issues I diagnosed were:

- System Error 5 / Access Denied when commands were not elevated
- Administrator group membership versus UAC elevation
- Permissions inherited from parent folders
- Users receiving access through group membership
- Broad Authenticated Users permissions allowing unintended access
- Explicit DENY permissions affecting administrator accounts
- Removing and restoring permissions
- Testing permissions from different user accounts
- Mapping, disconnecting and reconnecting a shared drive

### What I Learned

This lab helped me understand that Windows permissions are determined by a combination of user accounts, security groups, NTFS permissions, inheritance and UAC.

I also learned that troubleshooting permissions requires checking where access is actually coming from rather than assuming that a user has been granted access directly.

The most useful part of the lab was deliberately encountering Access Denied errors and then using tools such as `whoami`, `whoami /groups` and `icacls` to identify and correct the cause.
