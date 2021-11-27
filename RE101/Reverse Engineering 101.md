# LiveOverflow RE Tutorial

## 0x07 [Uncrackable Program](https://www.youtube.com/watch?v=qS4VWL5R_OM&list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN&index=9&ab_channel=LiveOverflow)

license_2.c source code

```C
#include <string.h>
#include <stdio.h>

int main(int argc, char *argv[]) {
        if(argc==2) {
                printf("Checking License: %s\n", argv[1]);
                int sum = 0;
                for (int i = 0; i < strlen(argv[1]); i++) {
                        sum+= (int)argv[1][i];
                }
                if(sum==916) {
                        printf("Access Granted!\n");
                } else {
                        printf("WRONG!\n");
                }
        } else {
                printf("Usage: <key>\n");
        }
        return 0;
}
```

# Compiling C Code

```bash
gcc license_2.c -std=c99 -o license_2
```


# Using "Strings" 
As the algorithm has changed, we couldn't find the license key using "strings"

```bash

└─# strings license_2 -n 10 

/lib64/ld-linux-x86-64.so.2
__cxa_finalize
__libc_start_main
GLIBC_2.2.5
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
[]A\A]A^A_
Checking License: %s
Access Granted!
Usage: <key>
GCC: (Debian 10.2.1-6) 10.2.1 20210110
/usr/lib/gcc/x86_64-linux-gnu/10/../../../x86_64-linux-gnu/Scrt1.o
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.0
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
license_2.c
__FRAME_END__
__init_array_end
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
puts@GLIBC_2.2.5
strlen@GLIBC_2.2.5
printf@GLIBC_2.2.5
__libc_start_main@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
__TMC_END__
_ITM_registerTMCloneTable
__cxa_finalize@GLIBC_2.2.5
.note.gnu.build-id
.note.ABI-tag
.gnu.version
.gnu.version_r
.eh_frame_hdr
.init_array
.fini_array

```


## radare2 
using radare2, run "aaa" to analyze all and navigate to the main function

```bash
└─# radare2 license_2                                                    
Warning: run r2 with -e io.cache=true to fix relocations in disassembly
[0x00001070]> aaa
[x] Analyze all flags starting with sym. and entry0 (aa)
[x] Analyze function calls (aac)
[x] Analyze len bytes of instructions for references (aar)
[x] Check for vtables
[x] Type matching analysis for all functions (aaft)
[x] Propagate noreturn information
[x] Use -AA or aaaa to perform additional experimental analysis.
[0x00001070]> afl
0x00001070    1 42           entry0
0x000010a0    4 41   -> 34   sym.deregister_tm_clones
0x000010d0    4 57   -> 51   sym.register_tm_clones
0x00001110    5 57   -> 50   sym.__do_global_dtors_aux
0x00001060    1 6            sym.imp.__cxa_finalize
0x00001150    1 5            entry.init0
0x00001000    3 23           sym._init
0x00001280    1 1            sym.__libc_csu_fini
0x00001284    1 9            sym._fini
0x00001220    4 93           sym.__libc_csu_init
0x00001155    9 195          main
0x00001030    1 6            sym.imp.puts
0x00001040    1 6            sym.imp.strlen
0x00001050    1 6            sym.imp.printf

[0x00001070]> s sym.main

[0x00001155]> pdf


```

**pdf to dissamble the program**

```bash
            ; DATA XREF from entry0 @ 0x108d
┌ 195: int main (uint32_t argc, char **argv);
│           ; var char **s @ rbp-0x30
│           ; var uint32_t var_24h @ rbp-0x24
│           ; var int64_t var_18h @ rbp-0x18
│           ; var uint32_t var_14h @ rbp-0x14
│           ; var int64_t var_8h @ rbp-0x8
│           ; arg uint32_t argc @ rdi
│           ; arg char **argv @ rsi
│           0x00001155      55             push rbp
│           0x00001156      4889e5         mov rbp, rsp
│           0x00001159      53             push rbx
│           0x0000115a      4883ec28       sub rsp, 0x28
│           0x0000115e      897ddc         mov dword [var_24h], edi    ; argc
│           0x00001161      488975d0       mov qword [s], rsi          ; argv
│           0x00001165      837ddc02       cmp dword [var_24h], 2
│       ┌─< 0x00001169      0f8592000000   jne 0x1201
│       │   0x0000116f      488b45d0       mov rax, qword [s]
│       │   0x00001173      4883c008       add rax, 8
│       │   0x00001177      488b00         mov rax, qword [rax]
│       │   0x0000117a      4889c6         mov rsi, rax
│       │   0x0000117d      488d3d800e00.  lea rdi, str.Checking_License:__s_n ; 0x2004 ; "Checking License: %s\n" ; const char *format
│       │   0x00001184      b800000000     mov eax, 0
│       │   0x00001189      e8c2feffff     call sym.imp.printf         ; int printf(const char *format)
│       │   0x0000118e      c745ec000000.  mov dword [var_14h], 0
│       │   0x00001195      c745e8000000.  mov dword [var_18h], 0
│      ┌──< 0x0000119c      eb20           jmp 0x11be
│      ││   ; CODE XREF from main @ 0x11da
│     ┌───> 0x0000119e      488b45d0       mov rax, qword [s]
│     ╎││   0x000011a2      4883c008       add rax, 8
│     ╎││   0x000011a6      488b10         mov rdx, qword [rax]
│     ╎││   0x000011a9      8b45e8         mov eax, dword [var_18h]
│     ╎││   0x000011ac      4898           cdqe
│     ╎││   0x000011ae      4801d0         add rax, rdx
│     ╎││   0x000011b1      0fb600         movzx eax, byte [rax]
│     ╎││   0x000011b4      0fbec0         movsx eax, al
│     ╎││   0x000011b7      0145ec         add dword [var_14h], eax
│     ╎││   0x000011ba      8345e801       add dword [var_18h], 1
│     ╎││   ; CODE XREF from main @ 0x119c
│     ╎└──> 0x000011be      8b45e8         mov eax, dword [var_18h]
│     ╎ │   0x000011c1      4863d8         movsxd rbx, eax
│     ╎ │   0x000011c4      488b45d0       mov rax, qword [s]
│     ╎ │   0x000011c8      4883c008       add rax, 8
│     ╎ │   0x000011cc      488b00         mov rax, qword [rax]
│     ╎ │   0x000011cf      4889c7         mov rdi, rax                ; const char *s                                                                                    
│     ╎ │   0x000011d2      e869feffff     call sym.imp.strlen         ; size_t strlen(const char *s)                                                                     
│     ╎ │   0x000011d7      4839c3         cmp rbx, rax
│     └───< 0x000011da      72c2           jb 0x119e
│       │   0x000011dc      817dec940300.  cmp dword [var_14h], 0x394
│      ┌──< 0x000011e3      750e           jne 0x11f3
│      ││   0x000011e5      488d3d2e0e00.  lea rdi, str.Access_Granted_ ; 0x201a ; "Access Granted!" ; const char *s                                                      
│      ││   0x000011ec      e83ffeffff     call sym.imp.puts           ; int puts(const char *s)                                                                          
│     ┌───< 0x000011f1      eb1a           jmp 0x120d
│     │││   ; CODE XREF from main @ 0x11e3
│     │└──> 0x000011f3      488d3d300e00.  lea rdi, str.WRONG_         ; 0x202a ; "WRONG!" ; const char *s                                                                
│     │ │   0x000011fa      e831feffff     call sym.imp.puts           ; int puts(const char *s)                                                                          
│     │┌──< 0x000011ff      eb0c           jmp 0x120d
│     │││   ; CODE XREF from main @ 0x1169
│     ││└─> 0x00001201      488d3d290e00.  lea rdi, str.Usage:__key_   ; 0x2031 ; "Usage: <key>" ; const char *s                                                          
│     ││    0x00001208      e823feffff     call sym.imp.puts           ; int puts(const char *s)                                                                          
│     ││    ; CODE XREFS from main @ 0x11f1, 0x11ff
│     └└──> 0x0000120d      b800000000     mov eax, 0
│           0x00001212      488b5df8       mov rbx, qword [var_8h]
│           0x00001216      c9             leave
└           0x00001217      c3             ret

```


# Run program in debug mode and add different arguments

```bash
[0x7fef453cc050]> 'ood AAAA-WRONG-KEY'
child received signal 9
Process with PID 1633 started...
= attach 1633 1633
File dbg:///home/kali/RE101/liveoverflow_youtube/0x07_0x08_uncrackable_crackme/license_2  AAAA-WRONG-KEY reopened in read-write mode
1633
[0x7f14d5947050]> 'dc'
Checking License: AAAA-WRONG-KEY
WRONG!
(1633) Process exited with status=0x0

```

*ood - open program in debug mode*
*dc - start program* 

# Setting breakpoint on interesting point

```bash

│      ┌──< 0x000011e3      750e           jne 0x11f3
│      ││   0x000011e5      488d3d2e0e00.  lea rdi, str.Access_Granted_ ; 0x201a ; "Access Granted!" ; const char *s

```

```bash
[0x00001155]> db 0x000011e3 
[0x00001155]> ood AAAA-TEST
Process with PID 1646 started...
= attach 1646 1646
File dbg:///home/kali/RE101/liveoverflow_youtube/0x07_0x08_uncrackable_crackme/license_2  AAAA-TEST reopened in read-write mode
1646
[0x7f75106bc050]> dc
Checking License: AAAA-TEST
hit breakpoint at: 0x55c3247de1e3

```

*db [address] to set breakpoint*

## Showing Registers content

```bash
[0x55fe528191e3]> dr
rax = 0x0000000e
rbx = 0x0000000e
rcx = 0x0000074d
rdx = 0x00004000
r8 = 0x7fe8856a9040
r9 = 0x7fe8856646f0
r10 = 0x55fe52818415
r11 = 0x7fe8855c3b20
r12 = 0x55fe52819070
r13 = 0x00000000
r14 = 0x00000000
r15 = 0x00000000
rsi = 0x55fe53a5a2a0
rdi = 0x7ffd1d0c374d
rsp = 0x7ffd1d0c2660
rbp = 0x7ffd1d0c2690
rip = 0x55fe528191e3
rflags = 0x00000202
orax = 0xffffffffffffffff
[0x55fe528191e3]> dr rip=0x55fe528191e5
0x55fe528191e3 ->0x55fe528191e5
[0x55fe528191e3]> dc
Access Granted!

```

 changing [rip] content using [dr]
 
 **calculate the address yourself**
 
 
### using "VV" to show program flow
[vv](Pasted image 20211117183143.png)

rename variable in VV mode
*afvn [variable_name] [new_variable_name]*

Mode to show all register info at the same time and debug

*Set breakpoints + run in debug mode*
*V!*



### writing python script to get keygen

```python
import random
def check_key(key):
    char_sum = 0
    for c in key:
        char_sum += ord(c)
    return char_sum

key = ""
while True:
    key += random.choice("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ-_")
    s = check_key(key)
    if s > 916:
        key = ""
    elif s == 916:
        print(f"key: {key}")

```



