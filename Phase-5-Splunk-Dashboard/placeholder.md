# Phase 5 — Splunk SOC Operations Dashboard

Built a multi-panel SOC Operations Dashboard in Splunk Enterprise using data 
collected from real attack sessions against hueylab.local. The dashboard provides 
real-time visibility into authentication events, account activity, failed logon 
attempts, attack traffic from the Kali Linux machine, and live syslog forwarding 
from the Kali attack machine.

## Dashboard Overview
![SOC Operations Dashboard Full View](SOC%20Operations%20Dashboard%20Full%20View.png)

## Dashboard Panels

1. Authentication Events Over Time — line chart showing logon activity across all sessions
![Authentication Events Over Time](Authentication%20Events%20Over%20Time.png)

2. Top Accounts by Logon Count — bar chart identifying most active accounts
![Top Accounts by Logon Count](Top%20Accounts%20by%20Logon%20Count.png)

3. Failed Logon Attempts — single value counter for brute force detection
![Failed Logon Attempts](Failed%20Logon%20Attempts.png)

4. Logons from Kali Attack Machine — forensic table showing all attack traffic
![Logons from Kali Attack Machine](Logons%20from%20Kali%20Attack%20Machine.png)

5. Kali Syslog — Live Attack Machine Logs — real-time table showing live syslog events forwarded from Kali Linux
![Kali Syslog Update](syslog%20update.png)

## Syslog Forwarding Configuration
Configured rsyslog on Kali Linux to forward all system logs to Splunk in real time:

- Installed rsyslog on Kali Linux: sudo apt install -y rsyslog
- Added forwarding rule to /etc/rsyslog.conf: *.* @192.168.99.10:514
- Opened UDP port 514 on Windows Server Firewall
- Configured Splunk UDP data input on port 514
- Verified logs flowing from 192.168.99.20 (Kali) to Splunk in real time

## SPL Queries Used
- Panel 1: index=main source="WinEventLog:Security" EventCode=4624 | timechart count by Account_Name
- Panel 2: index=main source="WinEventLog:Security" EventCode=4624 | stats count by Account_Name | sort -count | head 10
- Panel 3: index=main source="WinEventLog:Security" EventCode=4625 | stats count
- Panel 4: index=main source="WinEventLog:Security" EventCode=4624 Workstation_Name=kali | table _time, Account_Name, Workstation_Name, Logon_Type | sort -_time | head 20
- Panel 5: index=main source="udp:514" | table _time, host, _raw | sort -_time | head 20

## Author
Houston Jones | Atlanta, GA
GitHub: hjones360
Medium: medium.com/@agentjones
