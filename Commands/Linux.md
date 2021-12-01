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