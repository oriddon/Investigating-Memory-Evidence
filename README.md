# SBT-DF204 Case Study 3: Investigating Memory Evidence

**Course:** SBT-DF204 – Computer Forensics Case Studies
**Case Title:** Investigating Suspected Illegal File Transfer From Memory Evidence
**Environment:** Kali Linux (VMware Workstation)
**Forensic Tool:** Volatility Framework 2.6.1

## 📌 Project Overview

This project documents a digital forensic investigation into a suspected unauthorized file transfer using a Windows memory image named `memdumpWin7.mem`.

The investigation focused on recovering and examining evidence from computer memory to determine whether a document had been copied to an external storage device.

Using Volatility 2.6.1, I examined running processes, network connections, command history, Windows registry records, USB devices, user-account information, and File Explorer artefacts.

The findings were documented using labelled screenshots, an evidence log, and a reconstructed UTC timeline.

## 🎯 Investigation Objectives

The objectives of this investigation were to:

1. Identify and preserve the supplied memory image.
2. Verify evidence integrity using SHA-256 hashing.
3. Identify and validate the appropriate Windows memory profile.
4. Examine running processes and network connections.
5. Recover command history relating to possible file transfers.
6. Investigate USB devices and drive-letter assignments.
7. Analyse Windows user-profile and ShellBag records.
8. Reconstruct an evidence-supported timeline.
9. Present findings while acknowledging forensic limitations.

## 🛠️ Laboratory and Tools

The following tools were used:

* VMware Workstation
* Kali Linux
* Python 2.7.18
* Volatility Framework 2.6.1
* SHA-256 hashing utilities
* Linux terminal commands

### Volatility Plugins Used

* `imageinfo`
* `pslist`
* `psscan`
* `pstree`
* `hivelist`
* `netscan`
* `cmdscan`
* `consoles`
* `printkey`
* `shellbags`
* `getsids`

## 🔍 Investigation Methodology

The investigation began by identifying the supplied memory image and creating a forensic working copy.

SHA-256 hashing and byte-for-byte comparison confirmed that the working copy matched the original evidence.

The memory image was then examined using Volatility 2.6.1. The selected profile was:

`Win7SP1x86_23418`

Subsequent analysis focused on process activity, network records, command execution, removable-storage artefacts, and Windows user-profile information.

The recovered evidence was correlated to establish a defensible account of the suspected transfer.

## 📊 Key Findings

### 1. Command History

The examination recovered the following commands:

```cmd
cd Downloads
copy secret_file.docx F:
```

The corresponding console output displayed:

```text
1 file(s) copied.
```

This indicates that Windows reported a successful file-copy operation.

### 2. USB Storage Evidence

Registry analysis identified a storage device described as:

`Disk&Ven_General&Prod_UDisk&Rev_5.00`

Further examination of `MountedDevices` established a recorded association between drive F: and the General UDisk USB storage device.

### 3. User Account Evidence

The `getsids` plugin associated Command Prompt and Windows Explorer with the IEUser Windows account.

However, this evidence does not establish who was physically operating the computer.

### 4. ShellBag Evidence

ShellBag analysis recovered folder-history records referencing:

* `C:\Users\IEUser\Downloads`
* `F:\`

These records supported the relationship between the source directory and destination drive identified during command-history analysis.

### 5. Network Evidence

Network analysis identified browser-related endpoints, closed TCP connections, and an SSH service listening on port 22.

However, the available network records did not independently demonstrate that a file was transferred over the network.

## ⚠️ Investigation Limitations

The investigation was limited to the supplied memory image.

Although recovered console output reported a successful copy operation, the destination file was not independently recovered or examined.

Some recovered timestamps were inconsistent with the reported memory-image time, creating uncertainty in parts of the reconstructed timeline.

Additionally, the evidence could not establish whether the file-copy operation was authorized or identify the individual responsible.

## ✅ Conclusion

The investigation recovered evidence indicating that Windows reported successfully copying `secret_file.docx` from the Downloads directory to drive F:.

Windows registry records associated drive F: with a General UDisk USB storage device, while user-profile and ShellBag records provided further supporting context.

The findings strongly support a reported successful copy operation to USB-associated storage.

However, the investigation did not independently verify the copied file's contents or establish that the activity was unauthorized.

## 📁 Repository Contents

The investigation documentation includes:

* Forensic investigation report
* Labelled screenshots
* Volatility analysis results
* Evidence log (E01–E21)
* UTC forensic timeline
* Investigation findings and limitations

The original memory image and its forensic working copy are excluded from the repository.

## 🔐 Ethical Considerations

This investigation was conducted using authorized educational materials.

The analysis was performed offline, without contacting any remote hosts, accounts, or individuals identified in the evidence.

The investigation followed evidence-preservation principles and avoided conclusions that could not be supported by the recovered forensic artefacts.

## 📚 References

International Cybersecurity and Digital Forensics Academy (ICDFA).

SBT-DF204 – Computer Forensics Case Studies, Case Study 3: Investigating Memory Evidence.

---

**Project Type:** Academic Digital Forensics Investigation
**Course:** SBT-DF204
**Status:** Investigation Completed
