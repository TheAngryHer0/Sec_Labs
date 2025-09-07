# Port hardening lab
## OBJECTIVE: to secure open ports, most common one being port 445 for "server" under services.msc

## Commands
1. **Finding network address**
```cmd
ipconfig
```
```cmd
nmap -sS 192.168.68.59
```
```cmd
nmap -sS -p- 127.0.0.1
```

![image1](Sec_Labs/images/1.Port Hardening Lab/1.port 445 lab.png)


## Anomaly: Port still open after stopping in services.
1. **Lookup port status**
```cmd admin
netstat -ano | findstr :445
```
2. **check SMB protocol features**
```Powershell admin
Get-SmbServerConfiguration
```
3. **Disable SMB1 server protocol and disable server SMB2 config**
```Powershell admin
Disable-WindowsOptionFeature -online -FeatureNameSMB1Protocol
```
```Powershell admin
Set-SmbServerConfiguration-EnableSMB2Protocol $False
```
4. **Set firewall rule to block inbound TCP traffic at port 445**
```cmd admin
netsh advfirewall firewall add rule name="Block SMB 445" dir=in action=block protocol=TCP localport=445
```
5. **Check availability of SMB protocol**
```Powershell admin
Get-SMBserverconfiguration
```
6. **Check if still listed amongst open ports on Nmap**
```cmd
nmap -sS 192.168.68.59
```

## Port hardening of port 445 confirmed
