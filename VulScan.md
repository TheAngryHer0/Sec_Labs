# Vulnerability scan and mitigation
## Objective: to scan my own VM for vulnerabilities and ways to mitigate said vulnerabilities.

1. **NMAP vulnerability scan**

'''zsh
nmap -sV --script vulners 10.0.2.15
'''

with knowledge above, I can see that there is a vulnerable port open (port 8080)

2. **Port closing**

