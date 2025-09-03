# Port obfuscation Lab for port 22 and port 80
## OBJECTIVE: to obfuscate default ports to harden system and make it less predictable for guessing exploitable services.

## Port 22:

1. **using Kali VM, identify the current network address.**
```bash
ip a
```

2. **nmap to scan for open ports on current network address**
```bash
sudo nmap -sS -p- 127.0.0.1
```

3. **identified ssh, now to change listening port**
```bash
sudo nano /etc/ssh/sshd_config
```
**restarting ssh to confirm validitiy**
```bash
sudo systemctl restart ssh
```

4. **Check current listening ports (on 22 and 2222 specifically)**
```bash
sudo ss -tuln -p | grep 2222
