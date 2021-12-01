```bash
file <file_name>
```
//check file type
//LSB pie executable -> changes address everytime it runs (becareful setting breakpoints)

### what is syscalls and kernels ? 

```bash
The system call is the fundamental interface between an application and the Linux kernel.
```


### Beauty of Hexadecimals
using python to convert from binarry to hex

```python
# hexa
hex(123)
# binary
bin(123)
```

Big-endian vs Little Endian
![[Pasted image 20211201185932.png]]

// using python struct to deal with endian
```python
import struct

hex(struct.unpack("I", "ABCD")[0])
# output : 0x44434241

# switch endian
hex(struct.unpack(">I", "ABCD")[0])
# output : 0x41424344


# get binary strings
struck.pack("I", 0x41500000)
# output : \x00\x00PA'
```