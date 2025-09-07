# Generate and Manage Digital Certificates Using OpenSSL #
## OBJECTIVE: Create a self-signed certificate using OpenSSL to understand certificate management ##

1. **Generate personal private key**

*State requirements with openssl*

```bash
openssl genrsa -out private.key 2048
```

2. **Create digital certificate with private key**

```bash
openssl req -new -x509 -key private.key -out cert.pem -days 365
```
![prompts to ask for info that will be hashed with private key](images/3_DigitalCertLab/Lab3_1.png)

3. **Install certificate for future testing uses**

```bash
sudo cp cert.pem /usr/local/share/ca-certificates/cert.crt
```
![store for future use](images/3_DigitalCertLab/Lab3_2.png)

4. **Updating system for current available certs**

*trusts* the newly generated cert (for future test use)

```bash
sudo update-ca-certificates
```
![validates cert info for future use](images/3_DigitalCertLab/Lab3_3.png)

5. **openssl x509 -in cert.pem -text -noout**

*inspects the cert*

```bash
openssl x509 -in cert.pm -text -noout
```
![inspect cert](images/3_DigitalCertLab/Lab3_4.png)
