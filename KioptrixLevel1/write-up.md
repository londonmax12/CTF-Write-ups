# Kioptrix Level 1 Write-up
## Introduction
The Kioptrix Level 1 challenge is a vulnerable virtual machine designed to test penetration testing skills. The objective is to gain root access on the target machine using various tools and techniques.
## Exploits
1. **mod_ssl 2.8.4** - OpenFuck exploit [Source](https://github.com/exploit-inters/OpenFuck)
2. **Samba 2.2.1a** - trans2open overflow [Source](https://www.rapid7.com/db/modules/exploit/linux/samba/trans2open/)
## Tools used
- Nmap ``v7.94SVN``
- Nikto ``v2.5.0``
- Metasploit ``v6.4.1``
- OpenLuck [Source](https://github.com/heltonWernik/OpenLuck)
- Hydra ``v9.5``
## Method
1. **Discovery of IP Address**
    - Use ping command (ping 8.8.8.8) on the target machine to determine the source IP address.
2. **Enumeration**
    - Use Nmap to scan the target machine for open ports and services. Identify SMB and a website running Apache.
3. **Web Application Analysis**
    - Visit the website and analyze the default Apache webpage for potential vulnerabilities or information leakage.
4. **Vulnerability Scanning**
    - Use Nikto to scan the website for common vulnerabilities. Identify mod_ssl 2.8.4 and Apache 1.3.20 as potential targets for exploitation.
5. **Exploitation**
    - Use Metasploit to scan the SMB service and identify Samba 2.2.1a as the version running on the target.
    - Attempt to connect to the SMB shares using SMBClient and discover ADMIN\$ and IPC\$ shares. Attempt to access the ADMIN\$ share, requiring authentication.
6. **Samba Exploitation** 
    - Research the Samba version on Exploit-DB and find the trans2open overflow exploit.
    - Use Metasploit non-staged payload to exploit the Samba vulnerability and gain a root shell.
7. **OpenSSL Exploitation**
    - Discover that OpenSSL 2.8.4 is vulnerable to the OpenFuck exploit.
    - Download, compile, and run an updated version of the exploit from GitHub to gain another root shell.
8. **SSH Brute Force**
    - Attempt a brute force attack on SSH using Metasploit, but it does not yield any results.