## Create ROOT user and SWITCH to ROOT

```bash
┌─[parrot@parrot-vm]─[~/Desktop]
└──╼ $sudo passwd root
[sudo] password for parrot: 
New password: 
Retype new password: 
passwd: password updated successfully
```
### make file executable
```bash
chmod +x <file_name>
```

### create tar.gz file
```bash
tar -czvf flag.tar.gz \<directory_name> 
```
// look for tar upload exploit
e.g. [evilarc].(https://github.com/ptoomey3/evilarc)
e.g. zipslip writeups

```python
python2 evilarc.py -d 3 -o u -f flag.tar.gz util.py
```
// overwriting util.py to return bash output 
d = depth

### show ip
```bash
ifconfig -a
```

### make all files in folder 777

```bash
chmod 777 -R <folder_name>
```

### netstat
```
netstat -lntu
```

-l listening ports , -n port number, -t tcp ports, -u udp ports

### ufw firewall in linux
```
sudo ufw allow <port number> 
```

### how to allow ICMP packet in WSL
[Link to tutorial](https://superuser.com/questions/1449775/windows-wsl-2-cant-ping-host-machine/1496354)

### Writing CronJobs
```
Edit cronjobs
crontab -e

List all cronjobs
crontab -l 

Sample Command
00 12 * * * /usr/bin/git -C /root/covid19-public pull
```