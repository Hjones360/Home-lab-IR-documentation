# Phase 5 — Splunk SOC Operations Dashboard

Built a multi-panel SOC Operations Dashboard in Splunk Enterprise using data 
collected from real attack sessions against hueylab.local. The dashboard provides 
real-time visibility into authentication events, account activity, failed logon 
attempts, and attack traffic from the Kali Linux machine.

## Dashboard Overview
![SOC Operations Dashboard Full View](SOC%20Operations%20Dashboard%20Full%20View.png)

## Dashboard Panels

1. Authentication Events Over Time — line chart showing logon activity across all sessions
![Authentication Events Over Time](Authentication%20Events%20Over%20Time.png)

2. Top Accounts by Logon Count — bar chart identifying most active accounts
![Top Accounts by Logon Count](Top%20Accounts%20by%20Logon%20Count.png)

3. Failed Logon Attempts — single value counter for brute force detection
![Failed Logon Attempts](Failed%20Logon%20Attempts.png)

4. Logons from Kali
