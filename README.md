# Sec_Labs
Documenting my journey

:: Initial checks
netstat -ano | findstr :445
powershell -Command "Get-SmbServerConfiguration"
nmap -sS -p 445 127.0.0.1
nmap -sS -p 445 192.168.1.100

:: Fixes
net stop server
powershell -Command "Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol"
powershell -Command "Set-SmbServerConfiguration -EnableSMB2Protocol $false"
netsh advfirewall firewall add rule name="Block SMB 445" dir=in action=block protocol=TCP localport=445
shutdown /r /t 0

:: Verification
nmap -sS -p 445 192.168.1.100
netstat -ano | findstr :445
