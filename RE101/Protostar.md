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