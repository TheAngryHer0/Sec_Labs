# Vulnerability scan and mitigation
## Objective: to scan my own VM for vulnerabilities and ways to mitigate said vulnerabilities.

1. **NMAP vulnerability scan**

```bash
nmap -sV --script vulners 10.0.2.15
```
[](Sec_Labs/images/06_VulScan/vuls1.png)
*with knowledge above, I can see that there is a vulnerable port open (port 8080) with high vulnerability*


2. **Checking port service app**

```bash
sudo ss -tulnp | grep 8080
```
[](Sec_Labs/images/06_VulScan/vuls2.png)
*this gives the result that it is run by "apache2"*


3. **Disabling apache2**

```bash
sudo systemctl stop apache2
```
[](Sec_Labs/images/06_VulScan/vuls3.png)

4. **Updates to check for apache2 updates to software since exploit was recently reported**

```bash
sudo apt upgrade apache2
```
[](Sec_Labs/images/06_VulScan/vuls4.png)
*not enough space so revert to disabling service*


5. **Disable service and add defense in depth**

```bash
sudo systemctl disable apache2
sudo ufw deny 8080
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
sudo iptables -A INPUT -p udp --dport 8080 -j DROP
```
[](Sec_Labs/images/06_VulScan/vuls5.png)

6. **Verify secured port 8080**

[](Sec_Labs/images/06_VulScan/vuls_final.png)
```bash
nmap -p 8080 10.0.2.15
```

*Since current status is filtered, objective achieved.*

