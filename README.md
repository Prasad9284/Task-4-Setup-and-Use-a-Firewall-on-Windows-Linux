# Task 4-3 — Setup and Use a Firewall on Windows/Linux

## 📌 Objective
Configure and test basic firewall rules to allow or block network traffic using Windows Firewall or UFW on Linux.

---

## 🛠 Tools Used
- *Windows 10/11 PowerShell & Windows Defender Firewall*
- *Linux UFW (Uncomplicated Firewall)*
- Telnet / Netcat for testing

---

## 📝 Steps Performed

### 🔹 Windows (PowerShell)
1. Open *PowerShell as Administrator*.
2. List current inbound rules:
   ```powershell
   Get-NetFirewallRule | Where-Object {$_.Direction -eq 'Inbound'} |
     Format-Table DisplayName,Enabled,Action,Profile -AutoSize

3. Create inbound block rule for Port 23 (Telnet):

New-NetFirewallRule -DisplayName "Block Telnet Inbound" -Direction Inbound -Action Block -Protocol TCP -LocalPort 23


4. Verify the rule:

Get-NetFirewallRule -DisplayName "Block Telnet Inbound"


5. (Optional) Start Telnet service for testing:

sc config tlntsvr start= auto
Start-Service tlntsvr


6. Test the block:

Test-NetConnection -ComputerName localhost -Port 23


7. Remove the test rule:

Get-NetFirewallRule -DisplayName "Block Telnet Inbound" | Remove-NetFirewallRule




---

🔹 Linux (UFW)

1. Allow SSH first (if remote):

sudo ufw allow 22/tcp


2. Enable UFW:

sudo ufw enable


3. Block port 23:

sudo ufw deny 23/tcp


4. Verify:

sudo ufw status numbered


5. Test:

nc -vz localhost 23


6. Remove rule:

sudo ufw delete deny 23/tcp

📷 Screenshots

> Replace the image paths below with actual screenshot file paths in your repository.

1. Initial Firewall Rules 

2. Rule Added for Port 23 

3. Testing Blocked Port 

4. Final Firewall Status After Removal 


📖 Summary

A firewall is a network security system that monitors and controls incoming and outgoing traffic based on predetermined rules.

Stateful firewall: Tracks the state of active connections and makes decisions based on connection state.

Stateless firewall: Filters each packet individually without tracking connection state.

UFW: Simplifies iptables management in Linux.

Windows Firewall: Provides GUI and PowerShell options for granular rule control.


Blocking insecure ports like Telnet (port 23) prevents unauthorized access and reduces attack surfaces.


---

📂 Deliverables

README.md (this file)

Screenshots (/screenshots/ folder)

Exported configuration files:

Windows: firewall_backup.wfw

Linux: ufw_rules.txt

