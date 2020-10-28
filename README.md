# Developer CheatSheet
###### A useful set of commands for :penguin: developers 

---
#### Create bootable usb keys
>```bash
>sudo dd if=/path/to/your/isofile of=/your/usb/disk
>```

---
#### Compression/Decompression (tar)
>**Compress an entire directory or a single file**  
>```bash
>tar -czvf archive.tar.gz /path/to/directory-or-file
>```  

>**Compress multiple directories or files at once**
>```bash
>tar -czvf archive.tar.gz /home/ubuntu/Downloads /usr/local/stuff /home/ubuntu/Documents/notes.txt
>```

>**Compress excluding directories and files**
>```bash
>tar -czvf archive.tar.gz /home/ubuntu --exclude=/home/ubuntu/Downloads --exclude=/home/ubuntu/.cache
>```
>or
>```bash
>tar -czvf archive.tar.gz /home/ubuntu --exclude=*.mp4
>```  

>**Extract files**
>```bash
>tar -xzvf archive.tar.gz
>```  

>**Extract with output directory name**
>```bash
>tar -xzvf archive.tar.gz -C /tmp
>```  

>**See the content without extract**
>```bash
>tar -tvf archive.tar.gz
>```

---
#### SecureShell (ssh)
N.B.  
For all the following commands, the port can be excluded if the ssh service is running on default port (22)  
  
>**Key generation**
>```bash
>ssh-keygen
>```

>**ssh access**
>```bash
>ssh user@ip:port
>```
	
>**Automatic ssh access stubbing password (not good, use public/private key pair)**
>```bash
>sudo apt install sshpass
>sshpass -p password ssh user@ip:port
>```

>**Setup automatic ssh access with KeyPair**
>```bash
>ssh-copy-id user@ip:port
>ssh user@ip:port
>```

---
#### Secure Copy (scp)

>**Copy the file "foobar.txt" from a remote host to the local host**
>```bash
>scp username@ip:foobar.txt /some/local/directory 
>```

>**Copy the file "foobar.txt" from the local host to a remote host**
>```bash
>scp foobar.txt username@ip:/some/remote/directory 
>```

>**Copy the directory "foo" from the local host to a remote host's directory "bar"**
>```bash
>scp -r foo username@ip:/some/remote/directory/bar 
>```

>**Copy the file "foobar.txt" from remote host "ip1" to remote host "ip2"**
>```bash
>scp username@ip1:/some/remote/directory/foobar.txt username@ip2:/some/remote/directory/
>``` 

---
#### Networking    
 
##### Traffic analysis (tcpdump)

>**Dump all traffic**
>```bash
>sudo tcpdump
>```

>**Dump traffic for specific interface**
>```bash
>sudo tcpdump -i ens33
>```

>**Dump traffic for specific port port** 
>```bash
>sudo tcpdump port 8080
>```

>**Dump traffic for specific interface and port** 
>```bash
>sudo tcpdump -i ens33 port 8080
>```

>**Dump traffic for specific host**
>```bash
>sudo tcpdump host 192.168.1.130
>```

>**Dump traffic translating addresses**
>```bash
>sudo tcpdump -n
>```

>**Dump traffic writing to file**
>```bash
>sudo tcpdump -U -w dump.pcap
>```

>**Read file**
>```bash
>sudo tcpdump -r dump.pcap
>```  
&nbsp;

##### Show network info
>**ifconfig (deprecated)**
>```bash
>ifconfig
>```

>**ip (preferred)**
>```bash
>ip a
>```  
&nbsp;

##### Reversing
>**Reverse ip-address**
>```bash
>nslookup IP_ADDRESS
>```  

>**Reverse domain**
>```bash
>dig +short google.com
>```
&nbsp;

##### Routes
>**Show routes**
>```bash
>route -n
>```
>or
>```bash
>netstat -rn
>```
&nbsp;

##### Policies
>**Show policies**
>```bash
>sudo ip xfrm policy
>```  
&nbsp;

##### Ip tables
>**Show tables**
>```bash
>sudo iptables -S
>```
&nbsp;

##### Ip rules
>**Show rules**
>```bash
>sudo ip rule
>```
&nbsp;

##### Connections (nmcli)
>**Connect**
>```bash
>sudo nmcli con up id MY_CONNECTION
>```

>**Disconnect**
 >```bash
 >sudo nmcli con down id MY_CONNECTION
 >```
&nbsp;


##### Port scanning
>**"PING" specific TCP port**
>```bash
>nc -z -v -t 127.0.0.1 4789
>```

>**"PING" specific UDP port**
>```bash
>nc -z -v -u 127.0.0.1 4789
>```

>**More info TCP single port**
>```bash
>sudo nmap -Pn -p 4789 127.0.0.1
>```

>**More info UDP single port**
>```bash
>sudo nmap -Pn -sU -p 4789 127.0.0.1
>```

>**More info whole net**
>```bash
>sudo nmap -Pn 127.0.0.1
>```

>**Guess Operating System**
>```bash
>sudo nmap -O 127.0.0.1
>```

>**Find vulnerabilities (BONUS)**
>```bash
>sudo nmap -Pn -sV -sC 127.0.0.1
>```
&nbsp;

##### MAC address
>**Show MAC**
>```bash
>ip link show
>```

>**MAC spoofing**
>```bash
>ip link set eth0 down
>ip link set eth0 address 00:00:00:00:00:00
>ip link set eth0 up
>```

---
#### Docker  

##### Simple mode
>**Build image**  
>```docker build -t foo:0.0.1-SNAPSHOT .```

>**TAG image**  
>```docker tag foo:0.0.1-SNAPSHOT myregistry.it/project/foo:0.0.1-SNAPSHOT```

>**Registry Login**  
>```docker login -u <user> -p <password> myregistry.it```

>**Registry Logout**  
>```docker logout myregistry.it```

>**Push Image**  
>```docker push myregistry.it/project/foo:0.0.1-SNAPSHOT```

>**Inspect registry saved credentials**  
>```cat ~/.docker/config.json```

&nbsp;

##### Swarm mode  
>**Ports to open**  
>  - TCP 2366
>  - TCP 2377
>  - TCP_UDP 7946
>  - UDP 4789

>**Init swarm for manager node**  
>```docker swarm init```  
> This command register the current machine as Manager/Leader
	
>**Add manager**  
>```docker swarm join --token <TOKEN_RELEASED_AFTER_INIT> IP:2377```

>**Retrieve the manager token**  
>```docker swarm join-token manager```

>**Join workers**  
>```docker swarm join --token <Token released after the manager join> MANAGER_IP:2377```

>**Retrieve the token for joining workers (Run on the manager)**  

>```docker swarm join-token worker```

>**Show nodes from the manager**  
>```docker node ls```

>**Show services**  
>```docker service ls```

>**Remove services**  
>```docker service rm <service_name or service_id>```

>**Leave swarm**  
> **worker**    
>```docker swarm leave```    
>   
> **manager**    
>```docker swarm leave --force```    

>**Read services logs from manager**   
> **follow**        
>```docker service logs --follow <service_name or service_id>```    
>  
> **tail**       
>```docker service logs --tail 10 <service_name or service_id>```    
>  
> **all**    
>```docker service logs <service_name or service_id>```    
>  
> **since**    
>```docker service logs --since 60m <service_name or service_id>```    
>

---

#### MISC

##### Services/daemons (systemctl)
>**Enable auto startup**
>```bash
>sudo systemctl enable sshd
>```

>**Disable auto startup**
>```bash
>sudo systemctl disable sshd
>```

>**Start service**
>```bash
>sudo systemctl start sshd
>```

>**Stop service**
>```bash
>sudo systemctl stop sshd
>```

>**Restart service**
>```bash
>sudo systemctl restart sshd
>```

>**Status service**
>```bash
>sudo systemctl status sshd
>```

>**Reload configuration files**
>```bash
>sudo systemctl daemon-reload
>```
&nbsp;

##### Privileges
>```bash
>w
>whoami
>id
>```
&nbsp;

##### Permissions
>**Octal**  
>```stat -c "%a %n" <FILENAME> | awk '{print $1}'```

>**Symbolic**  
>```ls -la | grep <FILENAME> | awk '{print $1}'```  
>
&nbsp;


##### Swap space
>**Swap on disk**
>- Create a partition of preferred size (gparted)
>- Get the partition UUID
>```bash
>sudo blkid /dev/nvme0n1p3
>```
>- Modify /etc/fstab
>```bash
>UUID=a8db2b2e-9776-4178-b93e-357bae5dd0b1 none swap sw 0 0
>```
>- Reboot

>**Swap on file**
>- Disable exchanges   
>```sudo swapoff -a```  
>- Create swapfile  
>```sudo dd if=/dev/zero of=/swapfile bs=1M count=8192```  
>- Make the swapfile "swappable"  
>```sudo mkswap /swapfile```  
>- Turn on the swap  
>```sudo swapon /swapfile```    
>- Verify  
>```grep SwapTotal /proc/meminfo```

&nbsp;

##### Selinux
>**Show status**
>```bash
>sestatus
>```

>**Disable temporary**
>```bash
>sudo setenforce 0
>```

>**Disable permanent**
>```bash
>vim /etc/sysconfig/selinux
>```
>SELINUX=disabled

&nbsp;

