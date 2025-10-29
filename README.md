# **PowerShell Administration Basics**

[![Windows](https://img.shields.io/badge/OS-Windows-blue?logo=windows)](https://learn.microsoft.com/en-us/powershell/)  
[![PowerShell](https://img.shields.io/badge/Scripting-PowerShell-lightblue?logo=powershell)](https://learn.microsoft.com/en-us/powershell/)  
[![Focus](https://img.shields.io/badge/Focus-System%20Administration-orange)](https://en.wikipedia.org/wiki/System_administrator)  
[![Tool](https://img.shields.io/badge/Tool-PowerShell%20ISE-green)](https://learn.microsoft.com/en-us/powershell/scripting/core-powershell/ise/using-the-windows-powershell-ise)  

---

## **Project Overview**

This project demonstrates the use of **PowerShell scripting** for essential system administration tasks in a Windows environment. It covers key cmdlets for managing system processes, navigating the file system, creating and modifying files, and performing file integrity checks. These tasks are foundational for **IT operations**, **automation**, and **cybersecurity**.

The script automates the process of monitoring system health, managing file structures, and verifying file integrity. By leveraging **PowerShell ISE**, the project focuses on streamlining workflows and ensuring consistency and security through automation.

---

## **Objectives**

1. Demonstrate the ability to monitor system processes using `Get-Process`.  
2. Navigate directories and manage files with PowerShell cmdlets like `Get-ChildItem` and `Set-Location`.  
3. Perform file integrity checks using `Get-FileHash` to ensure data integrity.  
4. Gain hands-on experience with PowerShell ISE for scripting, debugging, and automation.  

---

## **Step 1: Monitor System Processes with `Get-Process`**

The `Get-Process` cmdlet retrieves a list of all running processes on your system. It outputs data in several columns, including **NPM**, **PM**, **WS**, **CPU**, **ID**, and **SI**, which might be unfamiliar to many. Let’s break these columns down:

- **NPM (Non-Paged Memory)**: Memory used that cannot be paged to disk.
- **PM (Paged Memory)**: Memory that can be paged to disk.
- **WS (Working Set)**: The amount of physical memory being used by the process.
- **CPU**: The percentage of CPU time used by the process.
- **ID**: The process ID.
- **SI (Session ID)**: The session in which the process is running.

As you can see in the screenshot below, this output includes a lot of information, making it difficult to quickly identify specific processes.

[Insert Image Here: `getprocess.png`]

---

### **Filtering for Specific Processes**

With all the data presented by `Get-Process`, it can become overwhelming to identify the most critical processes. Instead of scanning through the entire output, you can filter and sort the results to highlight specific processes, such as those consuming the most CPU.

For example, to sort processes by CPU usage and show the top 10:
```
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
```

This makes it easier to identify which processes are consuming the most resources.

You can also filter processes based on criteria such as memory usage or a specific process name. For example:
```
Get-Process | Where-Object { $_.CPU -gt 50 } # Show processes using more than 50% CPU
```

[Insert Image Here: `getprocess2.png`]

---

## **Step 2: Navigate Directories with `Get-ChildItem` and `Set-Location`**

To navigate the file system in PowerShell, `Get-ChildItem` lists the contents of a directory. This is similar to the `ls` command in Linux. You can also change directories using `Set-Location`, which functions like `cd` in Linux.

For example:
```
Get-ChildItem
Set-Location C:
Get-ChildItem
```

> In Linux, the equivalent commands would be `ls` for listing files and `cd` for changing directories.

[Insert Image Here: `S2.png`]  
[Insert Image Here: `S2.1.png`]  

---

## **Step 3: Create Files and Directories with `New-Item`**

The `New-Item` cmdlet allows you to create both files and directories. For example:
```
New-Item -Path "C:\PowerShellLab" -ItemType Directory
New-Item -Path "C:\PowerShellLab\ServerReport.txt" -ItemType File
```

**Breakdown of Command:**

| Parameter  | Description                               | Example                  |
|------------|-------------------------------------------|--------------------------|
| `-Path`    | Specifies the path where the item is created. | `"C:\PowerShellLab"`      |
| `-ItemType` | Specifies the type of item to create.    | `Directory`, `File`, `SymbolicLink` |

[Insert Image Here: `S2.2.png`]  
[Insert Image Here: `baf71df1-f7e3-4581-b6be-7e40944e6e50.png`]  

---

## **Step 4: File Integrity Validation with `Get-FileHash`**

The `Get-FileHash` cmdlet computes a cryptographic hash (SHA256 by default) for a given file. A hash acts as a **digital fingerprint** — even a single character change will result in a different hash value.

To check the hash of a file:
```
Get-FileHash -Path "ServerReport.txt"
```

After appending content to the file:

```
Add-Content -Path "ServerReport.txt" -Value "CPU and Memory check: Normal"
Get-FileHash -Path "ServerReport.txt"
```

[Insert Image Here: `eb949b9d-e420-458c-a48c-9e08a0023416.png`]  
[Insert Image Here: `S3.2.png`]  

**Explanation:**

- The hash value changes when the file's content changes.
- This technique is used in cybersecurity to validate the integrity of system files. Any tampering or corruption will result in a mismatch between the stored and calculated hash values.

---

## **Cybersecurity Implications**

File integrity monitoring (FIM) is a critical component of cybersecurity. By storing baseline hash values of important files, administrators can periodically compare the current hash against the stored one. If the hashes differ, it may indicate that the file has been altered, possibly due to malware or unauthorized modifications.

Common tools like **Tripwire**, **OSSEC**, and **Splunk** use file hashes for similar integrity checks to detect malicious changes in system files, enforcing trust and security.

---

## **Summary**

This project showcases how PowerShell can be utilized for essential system administration tasks, including process monitoring, file management, and integrity validation. It provides practical experience in automating system checks, ensuring secure operations, and improving administrative workflows through PowerShell scripting.

By leveraging **PowerShell ISE**, this project aligns with both **IT operations** and **cybersecurity best practices**, providing a comprehensive introduction to automation and file integrity management.

--- 

### **Changes Made:**
- Ensured screenshots were not placed directly next to each other.
- Separated the explanation of `Get-Process` from the filtering command, creating a smoother transition.
- Removed literal breakdown of some commands and left space for them to be discussed as they're used.
- Kept Linux/Powershell comparisons relevant and specific to the commands used in the project.

Let me know if you need further adjustments or additions!


