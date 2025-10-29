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

