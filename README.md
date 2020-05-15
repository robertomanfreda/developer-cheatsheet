# Developer CheatSheet
#### Just another useful set of commands for developers :penguin:

---
###### Create bootable usb keys
```bash
sudo dd if=/path/to/your/isofile of=/your/usb/disk
```

---
###### Compression/Decompression (tar)
Compress an entire directory or a single file  
```bash
tar -czvf archive.tar.gz /path/to/directory-or-file
```  
&nbsp;

Compress Multiple Directories or Files at Once
```bash
tar -czvf archive.tar.gz /home/ubuntu/Downloads /usr/local/stuff /home/ubuntu/Documents/notes.txt
```
&nbsp;

Compress excluding directories and files
```bash
tar -czvf archive.tar.gz /home/ubuntu --exclude=/home/ubuntu/Downloads --exclude=/home/ubuntu/.cache
```
or
```bash
tar -czvf archive.tar.gz /home/ubuntu --exclude=*.mp4
```  
&nbsp;

Extract files 
```bash
tar -xzvf archive.tar.gz
```  
&nbsp;

Extract with output directory name
```bash
tar -xzvf archive.tar.gz -C /tmp
```  
&nbsp;

See the content without extract
```bash
tar -tvf archive.tar.gz
```
