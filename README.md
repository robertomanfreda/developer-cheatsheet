# Developer CheatSheet
###### Just another useful set of commands for developers :penguin:

---
>##### Create bootable usb keys
```bash
sudo dd if=/path/to/your/isofile of=/your/usb/disk
```

---
>##### Compression/Decompression (tar)
**Compress an entire directory or a single file**  
```bash
tar -czvf archive.tar.gz /path/to/directory-or-file
```  

**Compress multiple directories or files at once**
```bash
tar -czvf archive.tar.gz /home/ubuntu/Downloads /usr/local/stuff /home/ubuntu/Documents/notes.txt
```

**Compress excluding directories and files**
```bash
tar -czvf archive.tar.gz /home/ubuntu --exclude=/home/ubuntu/Downloads --exclude=/home/ubuntu/.cache
```
or
```bash
tar -czvf archive.tar.gz /home/ubuntu --exclude=*.mp4
```  

**Extract files**
```bash
tar -xzvf archive.tar.gz
```  

**Extract with output directory name**
```bash
tar -xzvf archive.tar.gz -C /tmp
```  

**See the content without extract**
```bash
tar -tvf archive.tar.gz
```

---
>##### SecureShell (ssh)
N.B.  
For all the following commands, the port can be excluded if the ssh service is running on default port (22)  
  
**Key generation**
```bash
ssh-keygen
```

**ssh access**
```bash
ssh user@ip:port
```
	
**Automatic ssh access stubbing password (not good, use public/private key pair)**
```bash
sudo apt install sshpass
sshpass -p password ssh user@ip:port
```

**Setup automatic ssh access with KeyPair**
```bash
ssh-copy-id user@ip:port
ssh user@ip:port
```

---
>##### Secure Copy (scp)

**Copy the file "foobar.txt" from a remote host to the local host**
```bash
scp username@ip:foobar.txt /some/local/directory 
```

**Copy the file "foobar.txt" from the local host to a remote host**
```bash
scp foobar.txt username@ip:/some/remote/directory 
```

**Copy the directory "foo" from the local host to a remote host's directory "bar"**
```bash
scp -r foo username@ip:/some/remote/directory/bar 
```

**Copy the file "foobar.txt" from remote host "ip1" to remote host "ip2"**
```bash
scp username@ip1:/some/remote/directory/foobar.txt username@ip2:/some/remote/directory/
``` 

---
>##### Networking
>###### Traffic analysis (tcpdump)

**Dump all traffic**
```bash
sudo tcpdump
```

**Dump traffic for specific interface**
```bash
sudo tcpdump -i ens33
```

**Dump traffic for specific port port** 
```bash
sudo tcpdump port 8080
```

**Dump traffic for specific interface and port** 
```bash
sudo tcpdump -i ens33 port 8080
```

**Dump traffic ffor specific host**
```bash
sudo tcpdump host 192.168.1.130
```

**Dump traffic translating addresses**
```bash
sudo tcpdump -n
```

**Dump traffic writing to file**
```bash
sudo tcpdump -U -w dump.pcap
```

**Read file**
```bash
sudo tcpdump -r dump.pcap
```