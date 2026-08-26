# networkwalks-B082-WEEK3-PASSWORD-CRACKING-USING-JOHN-THE-RIPPER-JtR-
HOW TO CRACK HASHED PASSWORD IN A PDF/WORD FILE USING  JtR
# John the Ripper – Password Cracking Lab

## Overview

This project demonstrates how to use **John the Ripper (JtR)** to test the strength of passwords protecting an authorized lock/password file.

> **Important:** Use these techniques only on files, systems, or accounts that you own or have explicit permission to test.

## Objectives

* Install John the Ripper on windows or kali linux.
* use onlinehashing cracker to get the hashes from hashed pdf.
* Prepare the hash password using notepad.
* attack the file using john the ripper.
* recovered passwords.
* use the password to open the pdf.

## Requirements

* windows, Kali Linux or another Linux distribution
* John the Ripper(GUI)
* john the ripper(cli)browse it on john the ripper (GUI)  and paste the location of it from setting
* 
* An authorized password/hash file

* KALI LINUX 

## 1. Install John the Ripper

On Kali Linux:

```bash
sudo apt update
sudo apt install john
```

Verify the installation:

```bash
john --version
```

## 2. Check Supported Formats

To view formats supported by your installation:

```bash
john --list=formats
```

You can search for a particular format:

```bash
john --list=formats | grep -i zip
```

## 3. Prepare the Password File

Place your authorized password/hash file in your working directory.

Example:

```bash
mkdir ~/john-lab
cd ~/john-lab
```

For archive-based password testing, first extract the relevant hash representation using the appropriate John utility.

For example, for an authorized ZIP archive:

```bash
zip2john protected.zip > zip_hash.txt
```

For other supported file types, use the corresponding `*2john` utility available with your installation.

## 4. Dictionary Attack

John can use a wordlist to test passwords:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

If `rockyou.txt` is compressed, extract it first:

```bash
sudo gzip -d /usr/share/wordlists/rockyou.txt.gz
```

Then run:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```

## 5. Display Recovered Passwords

After John finishes:

```bash
john --show zip_hash.txt
```

This displays passwords that John has successfully recovered.

## 6. Resume an Interrupted Session

If the cracking process is interrupted:

```bash
john --restore
```

## 7. View the Cracking Session

You can check the status of a running John session with:

```bash
john --status
```

## 8. Using John Against a Specific Format

When the format is known, specify it explicitly:

```bash
john --format=<format> --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Example:

```bash
john --format=raw-sha256 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

## 9. Useful Commands

| Command                         | Purpose                      |
| ------------------------------- | ---------------------------- |
| `john --version`                | Display John version         |
| `john --list=formats`           | List supported formats       |
| `john --wordlist=<file> <hash>` | Run dictionary attack        |
| `john --show <hash>`            | Display recovered passwords  |
| `john --status`                 | Show current status          |
| `john --restore`                | Resume previous session      |
| `john --incremental <hash>`     | Incremental password testing |
| `john --help`                   | Display help                 |

## 10. Example Lab Workflow

```bash
# Create working directory
mkdir ~/john-lab
cd ~/john-lab

# Convert an authorized ZIP archive to a John-readable hash
zip2john protected.zip > zip_hash.txt

# Run a dictionary attack
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt

# Display recovered password
john --show zip_hash.txt
```

## Security Lessons

This lab demonstrates why strong passwords are important. Passwords that are short, common, or based on predictable words can potentially be discovered through dictionary attacks.

### Recommended Defenses

* Use long, unique passwords.
* Avoid common dictionary words.
* Use a password manager.
* Enable multi-factor authentication where available.
* Use strong password policies.
* Protect password hashes and encrypted files from unauthorized access.
* Monitor authentication attempts for suspicious activity.

## Disclaimer

AUTHOR: NICHOLAS KIPTOO C|EH
This repository is intended for **authorized cybersecurity education, penetration testing, CTFs, and password-strength auditing**. Do not use John the Ripper to access files, accounts, or systems without authorization.
