# To Simulate a DDOS SYN flooding and result of mitigation methods #
## Objective: Configure firewall rule via iptables to effectively block traffic ##

1. **check tcp ouput on Kali**
```bash
sudo tcpdump -i eth0 port 8080
```
![eth0 output at rest](images/5_MitigationLab/Lab5_0.png)
*at rest traffic*

2. **configure iptables rules for IB traffic**
```bash
sudo iptables -A INPUT -p tcp --dport 8080 -m limit --limit 10/min --limit-burst 20 -j ACCEPT
```
*below for excess traffic*
```bash
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```
![iptables rules on Kali](images/5_MitigationLab/Lab5_2_1.png)

3. **initial iptables output from rule configuration**
```bash
sudo iptables -L -n -v
```
![iptables output before flood](images/5_MitigationLab/Lab5_3.png)

4. **run hping3 on Ubuntu to simulate SYN packet flooding**
```bash
sudo hping3 -S -p 8080 --flood 10.0.2.15
```
![hping3 without flood](images/5_MitigationLab/Lab5_2.png)

5. **result iptables output after flood**
```bash
sudo iptables -L -n -v
```
![iptables output after flood](images/5_MitigationLab/Lab5_4.png)

