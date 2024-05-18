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
```PORT    STATE SERVICE
111/tcp open  rpcbind
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Apache httpd 2.4.52 ((Ubuntu))
|_http-title: Did not follow redirect to http://clicker.htb/
|_http-server-header: Apache/2.4.52 (Ubuntu)
111/tcp  open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      35595/tcp   mountd
|   100005  1,2,3      37073/tcp6  mountd
|   100005  1,2,3      57004/udp   mountd
|   100005  1,2,3      57841/udp6  mountd
|   100021  1,3,4      32991/tcp6  nlockmgr
|   100021  1,3,4      37845/tcp   nlockmgr
|   100021  1,3,4      52683/udp   nlockmgr
|   100021  1,3,4      55967/udp6  nlockmgr
|   100024  1          34955/tcp6  status
|   100024  1          45195/udp6  status
|   100024  1          51469/tcp   status
|   100024  1          54950/udp   status
|   100227  3           2049/tcp   nfs_acl
|_  100227  3           2049/tcp6  nfs_acl
2049/tcp open  nfs_acl 3 (RPC #100227)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
PORT      STATE SERVICE REASON
22/tcp    open  ssh     syn-ack ttl 63
80/tcp    open  http    syn-ack ttl 63
111/tcp   open  rpcbind syn-ack ttl 63
2049/tcp  open  nfs     syn-ack ttl 63
35595/tcp open  unknown syn-ack ttl 63
37845/tcp open  unknown syn-ack ttl 63
47997/tcp open  unknown syn-ack ttl 63
51469/tcp open  unknown syn-ack ttl 63
52481/tcp open  unknown syn-ack ttl 63
sudo nmap $ip -Pn -p- -sS --min-rate 5000 -vv -n





##no la he temrinado es larga pero de aqui saque el script de cookies para robarloas
htb
XPS-ass 
