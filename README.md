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

1. Monitor system processes and analyze their output.  
2. Navigate directories and manage files with PowerShell cmdlets (`Get-ChildItem`, `Set-Location`, `New-Item`, `Add-Content`, `Get-Content`).  
3. Ensure file integrity with `Get-FileHash` to verify data integrity.  
4. Gain practical experience with PowerShell ISE for scripting, debugging, and automation.

---

## **Step 1: Check System Processes**

The `Get-Process` cmdlet retrieves a list of all running processes on your system. It outputs data in several columns, such as **NPM**, **PM**, **WS**, **CPU**, **ID**, and **SI**, which might be unfamiliar to many. Here’s a screenshot of the output for reference:

<img width="710" height="1008" alt="image" src="https://github.com/user-attachments/assets/6b3802de-6b61-4a44-8666-c8ce45f0e80f" />

### **Explanation of Columns**:

- **NPM (Non-Paged Memory)**: Memory used that cannot be paged to disk.
- **PM (Paged Memory)**: Memory that can be paged to disk.
- **WS (Working Set)**: The amount of physical memory being used by the process.
- **CPU**: The percentage of CPU time used by the process.
- **ID**: The process ID.
- **SI (Session ID)**: The session in which the process is running.

As you can see in the screenshot, this output includes a lot of information, which might not be immediately clear. Now that you can see the data, we can filter and sort this output for better readability and relevance.

---

### **Filtering for Specifics**

Since `Get-Process` outputs a lot of data, it’s useful to filter the logs to focus on specific processes. For example, you might want to focus on processes that consume the most CPU! Here's how to filter the output to show only the top 10 processes by CPU usage:

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 10
```

<img width="722" height="247" alt="image" src="https://github.com/user-attachments/assets/a04dd8f0-1374-414b-9acc-29e723e350ef" />

You can also filter processes based on other criteria, such as name or memory usage! Here's an example:

- To filter for processes using more than 50% CPU:
  ```powershell
  Get-Process | Where-Object { $_.CPU -gt 50 }
  ```

<img width="627" height="296" alt="image" src="https://github.com/user-attachments/assets/aa4f8fdb-19e5-4c57-8c7f-9c4e41da3e6b" />

- To find processes with a specific name (e.g., the **best** broswer: `chrome`):
  ```powershell
  Get-Process | Where-Object { $_.Name -eq "chrome" }
  ```
  
<img width="565" height="386" alt="image" src="https://github.com/user-attachments/assets/2478318e-fafb-4039-93cf-707a4314dd2f" />

> Did anyone else notice the **bash code** being used here? This is very similar to how you'd filter processes in Linux by using commands like `ps` and `grep` or `awk`.

---

## **Step 2: Navigate Directories**

To navigate the file system in PowerShell, we start by listing the contents of the current directory using `Get-ChildItem`. This is similar to `ls` in Linux. If we want to change directories, we use `Set-Location`, which is also like `cd` in Linux.
> Both of these alternate commands do work in Window's Powershell!

For example, we may begin in the **D:** drive and want to switch to the **C:** drive:

- `Get-ChildItem`     # Check current directory
- `Set-Location C:\`  # Change to the C:\ drive
- `Get-ChildItem`     # List contents of the C:\ drive

In this sequence:
1. **`Get-ChildItem`** checks where we currently are (D: drive).
 
<img width="560" height="296" alt="image" src="https://github.com/user-attachments/assets/df44f9db-0b80-424b-ba5a-b3f0a636e5c0" />
> ""Before you judge my gaming reputar; I just haven't cleaned out my old files!

3. **`Set-Location C:\`** moves us to the **C:** drive.

<img width="201" height="39" alt="image" src="https://github.com/user-attachments/assets/d36fb255-bd82-42c7-92fe-7ad4b434a24b" />
   
5. **`Get-ChildItem`** lists the contents of the **C:** drive to verify the change.

<img width="633" height="311" alt="image" src="https://github.com/user-attachments/assets/def72f2d-372e-488d-933c-bd98b9c45dfb" />
> You can think of this as the **Linux `ls` and `cd` commands**, where you check the contents of a directory and move around the filesystem. PowerShell just uses different cmdlets (`Get-ChildItem` and `Set-Location`).

Pretty simple right?
---

## **Step 3: Create Files and Directories**

The `New-Item` cmdlet allows you to create both files and directories. For example:

```powershell
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

The `Get-FileHash` cmdlet computes a cryptographic hash (SHA256 by default) for a given file. A hash serves as a **digital fingerprint** — even a single change will result in a different hash value.

To check the hash of a file:
```powershell
Get-FileHash -Path "ServerReport.txt"
```

<img width="976" height="107" alt="image" src="https://github.com/user-attachments/assets/c0f945ab-12e9-414e-8ade-ef202de87374" />

After appending content to the file:
```powershell
Add-Content -Path "ServerReport.txt" -Value "CPU and Memory check: Normal"
Get-FileHash -Path "ServerReport.txt"
``` 

<img width="974" height="117" alt="image" src="https://github.com/user-attachments/assets/349c2524-cb09-4e0c-8e4a-5deaf53c1e92" />

**Explanation:**

- The hash value changes when the file's content changes.
- This technique is widely used in cybersecurity to validate the integrity of files and detect tampering.

---

## **Cybersecurity Implications**

File integrity monitoring (FIM) is a crucial aspect of cybersecurity. By storing baseline hash values of critical files, administrators can periodically compare the current hash against the stored one. If the hashes differ, it might indicate that the file has been tampered with, potentially due to malware or unauthorized modifications.

Common tools like **Tripwire**, **OSSEC**, and **Splunk** rely on similar techniques for integrity checking, ensuring that system files remain trusted and secure.

---

## **Summary**

This project highlights how PowerShell can be used for essential administrative tasks, such as checking system processes, managing files, and verifying file integrity. By automating these tasks with **PowerShell ISE**, the project improves system health checks, streamlines workflows, and supports security best practices.

Through this exercise, I gained hands-on experience with key PowerShell cmdlets like `Get-Process`, `Set-Location`, `New-Item`, and `Get-FileHash`, providing a solid foundation for **IT operations** and **cybersecurity**.

---

### **Changes Summary:**
- Removed command names from section headers.
- Separated screenshots logically with proper explanation.
- Reworked Linux/Powershell comparisons to be relevant and contextual.
- Smoothed transitions between sections and refined command explanations.

Let me know if this is aligned with your expectations now!
