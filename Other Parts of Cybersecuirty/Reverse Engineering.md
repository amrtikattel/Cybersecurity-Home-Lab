This is my own code that I am trying to reverse engineer using Ghidra & the commands to help with reverse engineering.
- file-identify the executable
- strings- find readable texts within the executable
- readelf-examine the ELF structure 
- objdump-examine the actual machine code
```c
#include <stdio.h>

int main(void){
	char character;
	int integer;
	double float_point_value;
	printf("Enter a character:");
	scanf("%c",&character);
	printf("\nEnter a integer:");
	scanf("%d",&integer);
	printf("\nEnter a floating-point value:");
	scanf("%lf",&float_point_value);
	printf("\nThe character you enterd is %c.\n",character);
	printf("The integer you entered is %d.\n",integer);
	printf("The floating-point value you enterd is %lf.\n",float_point_value);
	return 0;
}

```


### This is what happens after I run the file command.
```bash
Reverse Engineering Example: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=41dec6a8eb9d83cfd07faa98d8364afc2bab7abf, for GNU/Linux 4.4.0, not stripped
```

### This is what is printed after doing the strings command
```bash
[amrit@amrit-pc C Folder]$ strings hi
/lib64/ld-linux-x86-64.so.2
__stack_chk_fail
__isoc23_scanf
__libc_start_main
__cxa_finalize
printf
libc.so.6
GLIBC_2.38
GLIBC_2.2.5
GLIBC_2.4
GLIBC_2.34
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
PTE1
u3UH
Enter a character:
Enter a integer:
Enter a floating-point value:
The character you enterd is %c.
The integer you entered is %d.
The floating-point value you enterd is %lf.
;*3$"
GCC: (GNU) 16.1.1 20260728
Scrt1.o
__abi_tag
crtbeginS.o
deregister_tm_clones
__do_global_dtors_aux
completed.0
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
untitled.c
crtendS.o
__FRAME_END__
_DYNAMIC
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_start_main@GLIBC_2.34
_ITM_deregisterTMCloneTable
_edata
_fini
__stack_chk_fail@GLIBC_2.4
printf@GLIBC_2.2.5
__isoc23_scanf@GLIBC_2.38
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
_end
__bss_start
main
__TMC_END__
_ITM_registerTMCloneTable
__cxa_finalize@GLIBC_2.2.5
_init
.symtab
.strtab
.shstrtab
.note.gnu.build-id
.interp
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.sframe
.note.gnu.property
.note.ABI-tag
.init_array
.fini_array
.dynamic
.got
.got.plt
.data
.bss
.comment
```

### This is what happens after doing the readelf command

```bash 
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00 
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              DYN (Position-Independent  Executable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x1060
  Start of program headers:          64 (bytes into file)
  Start of section headers:          14104 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           56 (bytes)
  Number of program headers:         15
  Size of section headers:           64 (bytes)
  Number of section headers:         31
  Section header string table index: 30

```

### This is after doing the readelf -h hello command
```bash 
[amrit@amrit-pc C Folder]$ readelf -S hi
There are 31 section headers, starting at offset 0x3718:

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .note.gnu.bu[...] NOTE             0000000000000388  00000388
       0000000000000024  0000000000000000   A       0     0     4
  [ 2] .interp           PROGBITS         00000000000003ac  000003ac
       000000000000001c  0000000000000000   A       0     0     1
  [ 3] .gnu.hash         GNU_HASH         00000000000003c8  000003c8
       000000000000001c  0000000000000000   A       4     0     8
  [ 4] .dynsym           DYNSYM           00000000000003e8  000003e8
       00000000000000d8  0000000000000018   A       5     1     8
  [ 5] .dynstr           STRTAB           00000000000004c0  000004c0
       00000000000000c4  0000000000000000   A       0     0     1
  [ 6] .gnu.version      VERSYM           0000000000000584  00000584
       0000000000000012  0000000000000002   A       4     0     2
  [ 7] .gnu.version_r    VERNEED          0000000000000598  00000598
       0000000000000050  0000000000000000   A       5     1     8
  [ 8] .rela.dyn         RELA             00000000000005e8  000005e8
       00000000000000c0  0000000000000018   A       4     0     8
  [ 9] .rela.plt         RELA             00000000000006a8  000006a8
       0000000000000048  0000000000000018  AI       4    24     8
  [10] .init             PROGBITS         0000000000001000  00001000
       000000000000001b  0000000000000000  AX       0     0     4
  [11] .plt              PROGBITS         0000000000001020  00001020
       0000000000000040  0000000000000010  AX       0     0     16
  [12] .text             PROGBITS         0000000000001060  00001060
       000000000000020b  0000000000000000  AX       0     0     16
  [13] .fini             PROGBITS         000000000000126c  0000126c
       000000000000000d  0000000000000000  AX       0     0     4
  [14] .rodata           PROGBITS         0000000000002000  00002000
       00000000000000cd  0000000000000000   A       0     0     8
  [15] .eh_frame_hdr     PROGBITS         00000000000020d0  000020d0
       0000000000000024  0000000000000000   A       0     0     4
  [16] .eh_frame         PROGBITS         00000000000020f8  000020f8
       000000000000007c  0000000000000000   A       0     0     8
  [17] .sframe           GNU_SFRAME       0000000000002178  00002178
       000000000000006c  0000000000000000   A       0     0     8
  [18] .note.gnu.pr[...] NOTE             0000000000002200  00002200
       0000000000000040  0000000000000000   A       0     0     8
  [19] .note.ABI-tag     NOTE             0000000000002240  00002240
       0000000000000020  0000000000000000   A       0     0     4
  [20] .init_array       INIT_ARRAY       0000000000003dd0  00002dd0
       0000000000000008  0000000000000008  WA       0     0     8
  [21] .fini_array       FINI_ARRAY       0000000000003dd8  00002dd8
       0000000000000008  0000000000000008  WA       0     0     8
  [22] .dynamic          DYNAMIC          0000000000003de0  00002de0
       00000000000001e0  0000000000000010  WA       5     0     8
  [23] .got              PROGBITS         0000000000003fc0  00002fc0
       0000000000000028  0000000000000008  WA       0     0     8
  [24] .got.plt          PROGBITS         0000000000003fe8  00002fe8
       0000000000000030  0000000000000008  WA       0     0     8
  [25] .data             PROGBITS         0000000000004018  00003018
       0000000000000010  0000000000000000  WA       0     0     8
  [26] .bss              NOBITS           0000000000004028  00003028
       0000000000000008  0000000000000000  WA       0     0     1
  [27] .comment          PROGBITS         0000000000000000  00003028
       000000000000001b  0000000000000001  MS       0     0     1
  [28] .symtab           SYMTAB           0000000000000000  00003048
       0000000000000390  0000000000000018          29    18     8
  [29] .strtab           STRTAB           0000000000000000  000033d8
       0000000000000220  0000000000000000           0     0     1
  [30] .shstrtab         STRTAB           0000000000000000  000035f8
       000000000000011e  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  D (mbind), l (large), p (processor specific)
```


### This is what comes out after I do the objdump 
```bash
[amrit@amrit-pc C Folder]$ objdump -d hi

hi:     file format elf64-x86-64


Disassembly of section .init:

0000000000001000 <_init>:
    1000:       f3 0f 1e fa             endbr64
    1004:       48 83 ec 08             sub    $0x8,%rsp
    1008:       48 8b 05 c1 2f 00 00    mov    0x2fc1(%rip),%rax        # 3fd0 <__gmon_start__>
    100f:       48 85 c0                test   %rax,%rax
    1012:       74 02                   je     1016 <_init+0x16>
    1014:       ff d0                   call   *%rax
    1016:       48 83 c4 08             add    $0x8,%rsp
    101a:       c3                      ret

Disassembly of section .plt:

0000000000001020 <__stack_chk_fail@plt-0x10>:
    1020:       ff 35 ca 2f 00 00       push   0x2fca(%rip)        # 3ff0 <_GLOBAL_OFFSET_TABLE_+0x8>
    1026:       ff 25 cc 2f 00 00       jmp    *0x2fcc(%rip)        # 3ff8 <_GLOBAL_OFFSET_TABLE_+0x10>
    102c:       0f 1f 40 00             nopl   0x0(%rax)

0000000000001030 <__stack_chk_fail@plt>:
    1030:       ff 25 ca 2f 00 00       jmp    *0x2fca(%rip)        # 4000 <__stack_chk_fail@GLIBC_2.4>
    1036:       68 00 00 00 00          push   $0x0
    103b:       e9 e0 ff ff ff          jmp    1020 <_init+0x20>

0000000000001040 <printf@plt>:
    1040:       ff 25 c2 2f 00 00       jmp    *0x2fc2(%rip)        # 4008 <printf@GLIBC_2.2.5>
    1046:       68 01 00 00 00          push   $0x1
    104b:       e9 d0 ff ff ff          jmp    1020 <_init+0x20>

0000000000001050 <__isoc23_scanf@plt>:
    1050:       ff 25 ba 2f 00 00       jmp    *0x2fba(%rip)        # 4010 <__isoc23_scanf@GLIBC_2.38>
    1056:       68 02 00 00 00          push   $0x2
    105b:       e9 c0 ff ff ff          jmp    1020 <_init+0x20>

Disassembly of section .text:

0000000000001060 <_start>:
    1060:       f3 0f 1e fa             endbr64
    1064:       31 ed                   xor    %ebp,%ebp
    1066:       49 89 d1                mov    %rdx,%r9
    1069:       5e                      pop    %rsi
    106a:       48 89 e2                mov    %rsp,%rdx
    106d:       48 83 e4 f0             and    $0xfffffffffffffff0,%rsp
    1071:       50                      push   %rax
    1072:       54                      push   %rsp
    1073:       45 31 c0                xor    %r8d,%r8d
    1076:       31 c9                   xor    %ecx,%ecx
    1078:       48 8d 3d da 00 00 00    lea    0xda(%rip),%rdi        # 1159 <main>
    107f:       ff 15 3b 2f 00 00       call   *0x2f3b(%rip)        # 3fc0 <__libc_start_main@GLIBC_2.34>
    1085:       f4                      hlt
    1086:       66 2e 0f 1f 84 00 00    cs nopw 0x0(%rax,%rax,1)
    108d:       00 00 00 

0000000000001090 <deregister_tm_clones>:
    1090:       48 8d 3d 91 2f 00 00    lea    0x2f91(%rip),%rdi        # 4028 <__TMC_END__>
    1097:       48 8d 05 8a 2f 00 00    lea    0x2f8a(%rip),%rax        # 4028 <__TMC_END__>
    109e:       48 39 f8                cmp    %rdi,%rax
    10a1:       74 15                   je     10b8 <deregister_tm_clones+0x28>
    10a3:       48 8b 05 1e 2f 00 00    mov    0x2f1e(%rip),%rax        # 3fc8 <_ITM_deregisterTMCloneTable>
    10aa:       48 85 c0                test   %rax,%rax
    10ad:       74 09                   je     10b8 <deregister_tm_clones+0x28>
    10af:       ff e0                   jmp    *%rax
    10b1:       0f 1f 80 00 00 00 00    nopl   0x0(%rax)
    10b8:       c3                      ret
    10b9:       0f 1f 80 00 00 00 00    nopl   0x0(%rax)

00000000000010c0 <register_tm_clones>:
    10c0:       48 8d 3d 61 2f 00 00    lea    0x2f61(%rip),%rdi        # 4028 <__TMC_END__>
    10c7:       48 8d 35 5a 2f 00 00    lea    0x2f5a(%rip),%rsi        # 4028 <__TMC_END__>
    10ce:       48 29 fe                sub    %rdi,%rsi
    10d1:       48 89 f0                mov    %rsi,%rax
    10d4:       48 c1 ee 3f             shr    $0x3f,%rsi
    10d8:       48 c1 f8 03             sar    $0x3,%rax
    10dc:       48 01 c6                add    %rax,%rsi
    10df:       48 d1 fe                sar    $1,%rsi
    10e2:       74 14                   je     10f8 <register_tm_clones+0x38>
    10e4:       48 8b 05 ed 2e 00 00    mov    0x2eed(%rip),%rax        # 3fd8 <_ITM_registerTMCloneTable>
    10eb:       48 85 c0                test   %rax,%rax
    10ee:       74 08                   je     10f8 <register_tm_clones+0x38>
    10f0:       ff e0                   jmp    *%rax
    10f2:       66 0f 1f 44 00 00       nopw   0x0(%rax,%rax,1)
    10f8:       c3                      ret
    10f9:       0f 1f 80 00 00 00 00    nopl   0x0(%rax)

0000000000001100 <__do_global_dtors_aux>:
    1100:       f3 0f 1e fa             endbr64
    1104:       80 3d 1d 2f 00 00 00    cmpb   $0x0,0x2f1d(%rip)        # 4028 <__TMC_END__>
    110b:       75 33                   jne    1140 <__do_global_dtors_aux+0x40>
    110d:       55                      push   %rbp
    110e:       48 83 3d ca 2e 00 00    cmpq   $0x0,0x2eca(%rip)        # 3fe0 <__cxa_finalize@GLIBC_2.2.5>
    1115:       00 
    1116:       48 89 e5                mov    %rsp,%rbp
    1119:       74 0d                   je     1128 <__do_global_dtors_aux+0x28>
    111b:       48 8b 3d fe 2e 00 00    mov    0x2efe(%rip),%rdi        # 4020 <__dso_handle>
    1122:       ff 15 b8 2e 00 00       call   *0x2eb8(%rip)        # 3fe0 <__cxa_finalize@GLIBC_2.2.5>
    1128:       e8 63 ff ff ff          call   1090 <deregister_tm_clones>
    112d:       c6 05 f4 2e 00 00 01    movb   $0x1,0x2ef4(%rip)        # 4028 <__TMC_END__>
    1134:       5d                      pop    %rbp
    1135:       c3                      ret
    1136:       66 2e 0f 1f 84 00 00    cs nopw 0x0(%rax,%rax,1)
    113d:       00 00 00 
    1140:       c3                      ret
    1141:       0f 1f 40 00             nopl   0x0(%rax)
    1145:       66 66 2e 0f 1f 84 00    data16 cs nopw 0x0(%rax,%rax,1)
    114c:       00 00 00 00 

0000000000001150 <frame_dummy>:
    1150:       f3 0f 1e fa             endbr64
    1154:       e9 67 ff ff ff          jmp    10c0 <register_tm_clones>

0000000000001159 <main>:
    1159:       55                      push   %rbp
    115a:       48 89 e5                mov    %rsp,%rbp
    115d:       48 83 ec 20             sub    $0x20,%rsp
    1161:       64 48 8b 04 25 28 00    mov    %fs:0x28,%rax
    1168:       00 00 
    116a:       48 89 45 f8             mov    %rax,-0x8(%rbp)
    116e:       31 c0                   xor    %eax,%eax
    1170:       48 8d 05 91 0e 00 00    lea    0xe91(%rip),%rax        # 2008 <_IO_stdin_used+0x8>
    1177:       48 89 c7                mov    %rax,%rdi
    117a:       b8 00 00 00 00          mov    $0x0,%eax
    117f:       e8 bc fe ff ff          call   1040 <printf@plt>
    1184:       48 8d 45 eb             lea    -0x15(%rbp),%rax
    1188:       48 8d 15 8c 0e 00 00    lea    0xe8c(%rip),%rdx        # 201b <_IO_stdin_used+0x1b>
    118f:       48 89 c6                mov    %rax,%rsi
    1192:       48 89 d7                mov    %rdx,%rdi
    1195:       b8 00 00 00 00          mov    $0x0,%eax
    119a:       e8 b1 fe ff ff          call   1050 <__isoc23_scanf@plt>
    119f:       48 8d 05 78 0e 00 00    lea    0xe78(%rip),%rax        # 201e <_IO_stdin_used+0x1e>
    11a6:       48 89 c7                mov    %rax,%rdi
    11a9:       b8 00 00 00 00          mov    $0x0,%eax
    11ae:       e8 8d fe ff ff          call   1040 <printf@plt>
    11b3:       48 8d 45 ec             lea    -0x14(%rbp),%rax
    11b7:       48 8d 15 71 0e 00 00    lea    0xe71(%rip),%rdx        # 202f <_IO_stdin_used+0x2f>
    11be:       48 89 c6                mov    %rax,%rsi
    11c1:       48 89 d7                mov    %rdx,%rdi
    11c4:       b8 00 00 00 00          mov    $0x0,%eax
    11c9:       e8 82 fe ff ff          call   1050 <__isoc23_scanf@plt>
    11ce:       48 8d 05 5d 0e 00 00    lea    0xe5d(%rip),%rax        # 2032 <_IO_stdin_used+0x32>
    11d5:       48 89 c7                mov    %rax,%rdi
    11d8:       b8 00 00 00 00          mov    $0x0,%eax
    11dd:       e8 5e fe ff ff          call   1040 <printf@plt>
    11e2:       48 8d 45 f0             lea    -0x10(%rbp),%rax
    11e6:       48 8d 15 63 0e 00 00    lea    0xe63(%rip),%rdx        # 2050 <_IO_stdin_used+0x50>
    11ed:       48 89 c6                mov    %rax,%rsi
    11f0:       48 89 d7                mov    %rdx,%rdi
    11f3:       b8 00 00 00 00          mov    $0x0,%eax
    11f8:       e8 53 fe ff ff          call   1050 <__isoc23_scanf@plt>
    11fd:       0f b6 45 eb             movzbl -0x15(%rbp),%eax
    1201:       0f be c0                movsbl %al,%eax
    1204:       48 8d 15 4d 0e 00 00    lea    0xe4d(%rip),%rdx        # 2058 <_IO_stdin_used+0x58>
    120b:       89 c6                   mov    %eax,%esi
    120d:       48 89 d7                mov    %rdx,%rdi
    1210:       b8 00 00 00 00          mov    $0x0,%eax
    1215:       e8 26 fe ff ff          call   1040 <printf@plt>
    121a:       8b 45 ec                mov    -0x14(%rbp),%eax
    121d:       48 8d 15 5c 0e 00 00    lea    0xe5c(%rip),%rdx        # 2080 <_IO_stdin_used+0x80>
    1224:       89 c6                   mov    %eax,%esi
    1226:       48 89 d7                mov    %rdx,%rdi
    1229:       b8 00 00 00 00          mov    $0x0,%eax
    122e:       e8 0d fe ff ff          call   1040 <printf@plt>
    1233:       48 8b 45 f0             mov    -0x10(%rbp),%rax
    1237:       48 8d 15 62 0e 00 00    lea    0xe62(%rip),%rdx        # 20a0 <_IO_stdin_used+0xa0>
    123e:       66 48 0f 6e c0          movq   %rax,%xmm0
    1243:       48 89 d7                mov    %rdx,%rdi
    1246:       b8 01 00 00 00          mov    $0x1,%eax
    124b:       e8 f0 fd ff ff          call   1040 <printf@plt>
    1250:       b8 00 00 00 00          mov    $0x0,%eax
    1255:       48 8b 55 f8             mov    -0x8(%rbp),%rdx
    1259:       64 48 2b 14 25 28 00    sub    %fs:0x28,%rdx
    1260:       00 00 
    1262:       74 05                   je     1269 <main+0x110>
    1264:       e8 c7 fd ff ff          call   1030 <__stack_chk_fail@plt>
    1269:       c9                      leave
    126a:       c3                      ret

Disassembly of section .fini:

000000000000126c <_fini>:
    126c:       f3 0f 1e fa             endbr64
    1270:       48 83 ec 08             sub    $0x8,%rsp
    1274:       48 83 c4 08             add    $0x8,%rsp
    1278:       c3                      ret
```


### objdump -d -M intel hi
```bash
n
[amrit@amrit-pc C Folder]$ objdump -d -M intel hi

hi:     file format elf64-x86-64


Disassembly of section .init:

0000000000001000 <_init>:
    1000:       f3 0f 1e fa             endbr64
    1004:       48 83 ec 08             sub    rsp,0x8
    1008:       48 8b 05 c1 2f 00 00    mov    rax,QWORD PTR [rip+0x2fc1]        # 3fd0 <__gmon_start__>
    100f:       48 85 c0                test   rax,rax
    1012:       74 02                   je     1016 <_init+0x16>
    1014:       ff d0                   call   rax
    1016:       48 83 c4 08             add    rsp,0x8
    101a:       c3                      ret

Disassembly of section .plt:

0000000000001020 <__stack_chk_fail@plt-0x10>:
    1020:       ff 35 ca 2f 00 00       push   QWORD PTR [rip+0x2fca]        # 3ff0 <_GLOBAL_OFFSET_TABLE_+0x8>
    1026:       ff 25 cc 2f 00 00       jmp    QWORD PTR [rip+0x2fcc]        # 3ff8 <_GLOBAL_OFFSET_TABLE_+0x10>
    102c:       0f 1f 40 00             nop    DWORD PTR [rax+0x0]

0000000000001030 <__stack_chk_fail@plt>:
    1030:       ff 25 ca 2f 00 00       jmp    QWORD PTR [rip+0x2fca]        # 4000 <__stack_chk_fail@GLIBC_2.4>
    1036:       68 00 00 00 00          push   0x0
    103b:       e9 e0 ff ff ff          jmp    1020 <_init+0x20>

0000000000001040 <printf@plt>:
    1040:       ff 25 c2 2f 00 00       jmp    QWORD PTR [rip+0x2fc2]        # 4008 <printf@GLIBC_2.2.5>
    1046:       68 01 00 00 00          push   0x1
    104b:       e9 d0 ff ff ff          jmp    1020 <_init+0x20>

0000000000001050 <__isoc23_scanf@plt>:
    1050:       ff 25 ba 2f 00 00       jmp    QWORD PTR [rip+0x2fba]        # 4010 <__isoc23_scanf@GLIBC_2.38>
    1056:       68 02 00 00 00          push   0x2
    105b:       e9 c0 ff ff ff          jmp    1020 <_init+0x20>

Disassembly of section .text:

0000000000001060 <_start>:
    1060:       f3 0f 1e fa             endbr64
    1064:       31 ed                   xor    ebp,ebp
    1066:       49 89 d1                mov    r9,rdx
    1069:       5e                      pop    rsi
    106a:       48 89 e2                mov    rdx,rsp
    106d:       48 83 e4 f0             and    rsp,0xfffffffffffffff0
    1071:       50                      push   rax
    1072:       54                      push   rsp
    1073:       45 31 c0                xor    r8d,r8d
    1076:       31 c9                   xor    ecx,ecx
    1078:       48 8d 3d da 00 00 00    lea    rdi,[rip+0xda]        # 1159 <main>
    107f:       ff 15 3b 2f 00 00       call   QWORD PTR [rip+0x2f3b]        # 3fc0 <__libc_start_main@GLIBC_2.34>
    1085:       f4                      hlt
    1086:       66 2e 0f 1f 84 00 00    cs nop WORD PTR [rax+rax*1+0x0]
    108d:       00 00 00 

0000000000001090 <deregister_tm_clones>:
    1090:       48 8d 3d 91 2f 00 00    lea    rdi,[rip+0x2f91]        # 4028 <__TMC_END__>
    1097:       48 8d 05 8a 2f 00 00    lea    rax,[rip+0x2f8a]        # 4028 <__TMC_END__>
    109e:       48 39 f8                cmp    rax,rdi
    10a1:       74 15                   je     10b8 <deregister_tm_clones+0x28>
    10a3:       48 8b 05 1e 2f 00 00    mov    rax,QWORD PTR [rip+0x2f1e]        # 3fc8 <_ITM_deregisterTMCloneTable>
    10aa:       48 85 c0                test   rax,rax
    10ad:       74 09                   je     10b8 <deregister_tm_clones+0x28>
    10af:       ff e0                   jmp    rax
    10b1:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]
    10b8:       c3                      ret
    10b9:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]

00000000000010c0 <register_tm_clones>:
    10c0:       48 8d 3d 61 2f 00 00    lea    rdi,[rip+0x2f61]        # 4028 <__TMC_END__>
    10c7:       48 8d 35 5a 2f 00 00    lea    rsi,[rip+0x2f5a]        # 4028 <__TMC_END__>
    10ce:       48 29 fe                sub    rsi,rdi
    10d1:       48 89 f0                mov    rax,rsi
    10d4:       48 c1 ee 3f             shr    rsi,0x3f
    10d8:       48 c1 f8 03             sar    rax,0x3
    10dc:       48 01 c6                add    rsi,rax
    10df:       48 d1 fe                sar    rsi,1
    10e2:       74 14                   je     10f8 <register_tm_clones+0x38>
    10e4:       48 8b 05 ed 2e 00 00    mov    rax,QWORD PTR [rip+0x2eed]        # 3fd8 <_ITM_registerTMCloneTable>
    10eb:       48 85 c0                test   rax,rax
    10ee:       74 08                   je     10f8 <register_tm_clones+0x38>
    10f0:       ff e0                   jmp    rax
    10f2:       66 0f 1f 44 00 00       nop    WORD PTR [rax+rax*1+0x0]
    10f8:       c3                      ret
    10f9:       0f 1f 80 00 00 00 00    nop    DWORD PTR [rax+0x0]

0000000000001100 <__do_global_dtors_aux>:
    1100:       f3 0f 1e fa             endbr64
    1104:       80 3d 1d 2f 00 00 00    cmp    BYTE PTR [rip+0x2f1d],0x0        # 4028 <__TMC_END__>
    110b:       75 33                   jne    1140 <__do_global_dtors_aux+0x40>
    110d:       55                      push   rbp
    110e:       48 83 3d ca 2e 00 00    cmp    QWORD PTR [rip+0x2eca],0x0        # 3fe0 <__cxa_finalize@GLIBC_2.2.5>
    1115:       00 
    1116:       48 89 e5                mov    rbp,rsp
    1119:       74 0d                   je     1128 <__do_global_dtors_aux+0x28>
    111b:       48 8b 3d fe 2e 00 00    mov    rdi,QWORD PTR [rip+0x2efe]        # 4020 <__dso_handle>
    1122:       ff 15 b8 2e 00 00       call   QWORD PTR [rip+0x2eb8]        # 3fe0 <__cxa_finalize@GLIBC_2.2.5>
    1128:       e8 63 ff ff ff          call   1090 <deregister_tm_clones>
    112d:       c6 05 f4 2e 00 00 01    mov    BYTE PTR [rip+0x2ef4],0x1        # 4028 <__TMC_END__>
    1134:       5d                      pop    rbp
    1135:       c3                      ret
    1136:       66 2e 0f 1f 84 00 00    cs nop WORD PTR [rax+rax*1+0x0]
    113d:       00 00 00 
    1140:       c3                      ret
    1141:       0f 1f 40 00             nop    DWORD PTR [rax+0x0]
    1145:       66 66 2e 0f 1f 84 00    data16 cs nop WORD PTR [rax+rax*1+0x0]
    114c:       00 00 00 00 

0000000000001150 <frame_dummy>:
    1150:       f3 0f 1e fa             endbr64
    1154:       e9 67 ff ff ff          jmp    10c0 <register_tm_clones>

0000000000001159 <main>:
    1159:       55                      push   rbp
    115a:       48 89 e5                mov    rbp,rsp
    115d:       48 83 ec 20             sub    rsp,0x20
    1161:       64 48 8b 04 25 28 00    mov    rax,QWORD PTR fs:0x28
    1168:       00 00 
    116a:       48 89 45 f8             mov    QWORD PTR [rbp-0x8],rax
    116e:       31 c0                   xor    eax,eax
    1170:       48 8d 05 91 0e 00 00    lea    rax,[rip+0xe91]        # 2008 <_IO_stdin_used+0x8>
    1177:       48 89 c7                mov    rdi,rax
    117a:       b8 00 00 00 00          mov    eax,0x0
    117f:       e8 bc fe ff ff          call   1040 <printf@plt>
    1184:       48 8d 45 eb             lea    rax,[rbp-0x15]
    1188:       48 8d 15 8c 0e 00 00    lea    rdx,[rip+0xe8c]        # 201b <_IO_stdin_used+0x1b>
    118f:       48 89 c6                mov    rsi,rax
    1192:       48 89 d7                mov    rdi,rdx
    1195:       b8 00 00 00 00          mov    eax,0x0
    119a:       e8 b1 fe ff ff          call   1050 <__isoc23_scanf@plt>
    119f:       48 8d 05 78 0e 00 00    lea    rax,[rip+0xe78]        # 201e <_IO_stdin_used+0x1e>
    11a6:       48 89 c7                mov    rdi,rax
    11a9:       b8 00 00 00 00          mov    eax,0x0
    11ae:       e8 8d fe ff ff          call   1040 <printf@plt>
    11b3:       48 8d 45 ec             lea    rax,[rbp-0x14]
    11b7:       48 8d 15 71 0e 00 00    lea    rdx,[rip+0xe71]        # 202f <_IO_stdin_used+0x2f>
    11be:       48 89 c6                mov    rsi,rax
    11c1:       48 89 d7                mov    rdi,rdx
    11c4:       b8 00 00 00 00          mov    eax,0x0
    11c9:       e8 82 fe ff ff          call   1050 <__isoc23_scanf@plt>
    11ce:       48 8d 05 5d 0e 00 00    lea    rax,[rip+0xe5d]        # 2032 <_IO_stdin_used+0x32>
    11d5:       48 89 c7                mov    rdi,rax
    11d8:       b8 00 00 00 00          mov    eax,0x0
    11dd:       e8 5e fe ff ff          call   1040 <printf@plt>
    11e2:       48 8d 45 f0             lea    rax,[rbp-0x10]
    11e6:       48 8d 15 63 0e 00 00    lea    rdx,[rip+0xe63]        # 2050 <_IO_stdin_used+0x50>
    11ed:       48 89 c6                mov    rsi,rax
    11f0:       48 89 d7                mov    rdi,rdx
    11f3:       b8 00 00 00 00          mov    eax,0x0
    11f8:       e8 53 fe ff ff          call   1050 <__isoc23_scanf@plt>
    11fd:       0f b6 45 eb             movzx  eax,BYTE PTR [rbp-0x15]
    1201:       0f be c0                movsx  eax,al
    1204:       48 8d 15 4d 0e 00 00    lea    rdx,[rip+0xe4d]        # 2058 <_IO_stdin_used+0x58>
    120b:       89 c6                   mov    esi,eax
    120d:       48 89 d7                mov    rdi,rdx
    1210:       b8 00 00 00 00          mov    eax,0x0
    1215:       e8 26 fe ff ff          call   1040 <printf@plt>
    121a:       8b 45 ec                mov    eax,DWORD PTR [rbp-0x14]
    121d:       48 8d 15 5c 0e 00 00    lea    rdx,[rip+0xe5c]        # 2080 <_IO_stdin_used+0x80>
    1224:       89 c6                   mov    esi,eax
    1226:       48 89 d7                mov    rdi,rdx
    1229:       b8 00 00 00 00          mov    eax,0x0
    122e:       e8 0d fe ff ff          call   1040 <printf@plt>
    1233:       48 8b 45 f0             mov    rax,QWORD PTR [rbp-0x10]
    1237:       48 8d 15 62 0e 00 00    lea    rdx,[rip+0xe62]        # 20a0 <_IO_stdin_used+0xa0>
    123e:       66 48 0f 6e c0          movq   xmm0,rax
    1243:       48 89 d7                mov    rdi,rdx
    1246:       b8 01 00 00 00          mov    eax,0x1
    124b:       e8 f0 fd ff ff          call   1040 <printf@plt>
    1250:       b8 00 00 00 00          mov    eax,0x0
    1255:       48 8b 55 f8             mov    rdx,QWORD PTR [rbp-0x8]
    1259:       64 48 2b 14 25 28 00    sub    rdx,QWORD PTR fs:0x28
    1260:       00 00 
    1262:       74 05                   je     1269 <main+0x110>
    1264:       e8 c7 fd ff ff          call   1030 <__stack_chk_fail@plt>
    1269:       c9                      leave
    126a:       c3                      ret

Disassembly of section .fini:

000000000000126c <_fini>:
    126c:       f3 0f 1e fa             endbr64
    1270:       48 83 ec 08             sub    rsp,0x8
    1274:       48 83 c4 08             add    rsp,0x8
    1278:       c3                      ret

```

### objdump -h hi
```bash 
amrit@amrit-pc C Folder]$ objdump -h hi

hi:     file format elf64-x86-64

Sections:
Idx Name          Size      VMA               LMA               File off  Algn
  0 .note.gnu.build-id 00000024  0000000000000388  0000000000000388  00000388  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  1 .interp       0000001c  00000000000003ac  00000000000003ac  000003ac  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  2 .gnu.hash     0000001c  00000000000003c8  00000000000003c8  000003c8  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  3 .dynsym       000000d8  00000000000003e8  00000000000003e8  000003e8  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  4 .dynstr       000000c4  00000000000004c0  00000000000004c0  000004c0  2**0
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  5 .gnu.version  00000012  0000000000000584  0000000000000584  00000584  2**1
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  6 .gnu.version_r 00000050  0000000000000598  0000000000000598  00000598  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  7 .rela.dyn     000000c0  00000000000005e8  00000000000005e8  000005e8  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  8 .rela.plt     00000048  00000000000006a8  00000000000006a8  000006a8  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
  9 .init         0000001b  0000000000001000  0000000000001000  00001000  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
 10 .plt          00000040  0000000000001020  0000000000001020  00001020  2**4
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
 11 .text         0000020b  0000000000001060  0000000000001060  00001060  2**4
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
 12 .fini         0000000d  000000000000126c  000000000000126c  0000126c  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, CODE
 13 .rodata       000000cd  0000000000002000  0000000000002000  00002000  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
 14 .eh_frame_hdr 00000024  00000000000020d0  00000000000020d0  000020d0  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
 15 .eh_frame     0000007c  00000000000020f8  00000000000020f8  000020f8  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
 16 .sframe       0000006c  0000000000002178  0000000000002178  00002178  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
 17 .note.gnu.property 00000040  0000000000002200  0000000000002200  00002200  2**3
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
 18 .note.ABI-tag 00000020  0000000000002240  0000000000002240  00002240  2**2
                  CONTENTS, ALLOC, LOAD, READONLY, DATA
 19 .init_array   00000008  0000000000003dd0  0000000000003dd0  00002dd0  2**3
                  CONTENTS, ALLOC, LOAD, DATA
 20 .fini_array   00000008  0000000000003dd8  0000000000003dd8  00002dd8  2**3
                  CONTENTS, ALLOC, LOAD, DATA
 21 .dynamic      000001e0  0000000000003de0  0000000000003de0  00002de0  2**3
                  CONTENTS, ALLOC, LOAD, DATA
 22 .got          00000028  0000000000003fc0  0000000000003fc0  00002fc0  2**3
                  CONTENTS, ALLOC, LOAD, DATA
 23 .got.plt      00000030  0000000000003fe8  0000000000003fe8  00002fe8  2**3
                  CONTENTS, ALLOC, LOAD, DATA
 24 .data         00000010  0000000000004018  0000000000004018  00003018  2**3
                  CONTENTS, ALLOC, LOAD, DATA
 25 .bss          00000008  0000000000004028  0000000000004028  00003028  2**0
                  ALLOC
 26 .comment      0000001b  0000000000000000  0000000000000000  00003028  2**0
                  CONTENTS, READONLY

```

### objdump -t hi
```bash
amrit@amrit-pc C Folder]$ objdump -t hi

hi:     file format elf64-x86-64

SYMBOL TABLE:
0000000000000000 l    df *ABS*  0000000000000000              Scrt1.o
0000000000002240 l     O .note.ABI-tag  0000000000000020              __abi_tag
0000000000000000 l    df *ABS*  0000000000000000              crtbeginS.o
0000000000001090 l     F .text  0000000000000000              deregister_tm_clones
00000000000010c0 l     F .text  0000000000000000              register_tm_clones
0000000000001100 l     F .text  0000000000000000              __do_global_dtors_aux
0000000000004028 l     O .bss   0000000000000001              completed.0
0000000000003dd8 l     O .fini_array    0000000000000000              __do_global_dtors_aux_fini_array_entry
0000000000001150 l     F .text  0000000000000000              frame_dummy
0000000000003dd0 l     O .init_array    0000000000000000              __frame_dummy_init_array_entry
0000000000000000 l    df *ABS*  0000000000000000              untitled.c
0000000000000000 l    df *ABS*  0000000000000000              crtendS.o
0000000000002170 l     O .eh_frame      0000000000000000              __FRAME_END__
0000000000000000 l    df *ABS*  0000000000000000              
0000000000003de0 l     O .dynamic       0000000000000000              _DYNAMIC
00000000000020d0 l       .eh_frame_hdr  0000000000000000              __GNU_EH_FRAME_HDR
0000000000003fe8 l     O .got.plt       0000000000000000              _GLOBAL_OFFSET_TABLE_
0000000000000000       F *UND*  0000000000000000              __libc_start_main@GLIBC_2.34
0000000000000000  w      *UND*  0000000000000000              _ITM_deregisterTMCloneTable
0000000000004018  w      .data  0000000000000000              data_start
0000000000004028 g       .data  0000000000000000              _edata
000000000000126c g     F .fini  0000000000000000              .hidden _fini
0000000000000000       F *UND*  0000000000000000              __stack_chk_fail@GLIBC_2.4
0000000000000000       F *UND*  0000000000000000              printf@GLIBC_2.2.5
0000000000000000       F *UND*  0000000000000000              __isoc23_scanf@GLIBC_2.38
0000000000004018 g       .data  0000000000000000              __data_start
0000000000000000  w      *UND*  0000000000000000              __gmon_start__
0000000000004020 g     O .data  0000000000000000              .hidden __dso_handle
0000000000002000 g     O .rodata        0000000000000004              _IO_stdin_used
0000000000004030 g       .bss   0000000000000000              _end
0000000000001060 g     F .text  0000000000000026              _start
0000000000004028 g       .bss   0000000000000000              __bss_start
0000000000001159 g     F .text  0000000000000112              main
0000000000004028 g     O .data  0000000000000000              .hidden __TMC_END__
0000000000000000  w      *UND*  0000000000000000              _ITM_registerTMCloneTable
0000000000000000  w    F *UND*  0000000000000000              __cxa_finalize@GLIBC_2.2.5
0000000000001000 g     F .init  0000000000000000              .hidden _init
```

### objdump -t hello | grep main
```bash
[amrit@amrit-pc C Folder]$ objdump -t hi | grep main
0000000000000000       F *UND*  0000000000000000              __libc_start_main@GLIBC_2.34
0000000000001159 g     F .text  0000000000000112              main
```



### This is it after being stripped
```bash 
[amrit@amrit-pc C Folder]$ ls 
hi  untitled.c  untitled.o
[amrit@amrit-pc C Folder]$ strip hi
[amrit@amrit-pc C Folder]$ ls 
hi  untitled.c  untitled.o
[amrit@amrit-pc C Folder]$ file hi
hi: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=41dec6a8eb9d83cfd07faa98d8364afc2bab7abf, for GNU/Linux 4.4.0, stripped
[amrit@amrit-pc C Folder]$ readelf -S hi
There are 29 section headers, starting at offset 0x3158:

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .note.gnu.bu[...] NOTE             0000000000000388  00000388
       0000000000000024  0000000000000000   A       0     0     4
  [ 2] .interp           PROGBITS         00000000000003ac  000003ac
       000000000000001c  0000000000000000   A       0     0     1
  [ 3] .gnu.hash         GNU_HASH         00000000000003c8  000003c8
       000000000000001c  0000000000000000   A       4     0     8
  [ 4] .dynsym           DYNSYM           00000000000003e8  000003e8
       00000000000000d8  0000000000000018   A       5     1     8
  [ 5] .dynstr           STRTAB           00000000000004c0  000004c0
       00000000000000c4  0000000000000000   A       0     0     1
  [ 6] .gnu.version      VERSYM           0000000000000584  00000584
       0000000000000012  0000000000000002   A       4     0     2
  [ 7] .gnu.version_r    VERNEED          0000000000000598  00000598
       0000000000000050  0000000000000000   A       5     1     8
  [ 8] .rela.dyn         RELA             00000000000005e8  000005e8
       00000000000000c0  0000000000000018   A       4     0     8
  [ 9] .rela.plt         RELA             00000000000006a8  000006a8
[amrit@amrit-pc C Folder]$ amrit@amrit-pc C Folder]$ file hi
hi: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=41dec6a8eb9d83cfd07faa98d8364afc2bab7abf, for GNU/Linux 4.4.0, stripped
[amrit@amrit-pc C Folder]$ readelf -S hi
There are 29 section headers, starting at offset 0x3158:

Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000
       0000000000000000  0000000000000000           0     0     0
  [ 1] .note.gnu.bu[...] NOTE             0000000000000388  00000388
       0000000000000024  0000000000000000   A       0     0     4
  [ 2] .interp           PROGBITS         00000000000003ac  000003ac
       000000000000001c  0000000000000000   A       0     0     1
  [ 3] .gnu.hash         GNU_HASH         00000000000003c8  000003c8
       000000000000001c  0000000000000000   A       4     0     8
  [ 4] .dynsym           DYNSYM           00000000000003e8  000003e8
       00000000000000d8  0000000000000018   A       5     1     8
  [ 5] .dynstr           STRTAB           00000000000004c0  000004c0
       00000000000000c4  0000000000000000   A       0     0     1
  [ 6] .gnu.version      VERSYM           0000000000000584  00000584
       0000000000000012  0000000000000002   A       4     0     2
  [ 7] .gnu.version_r    VERNEED          0000000000000598  00000598
       0000000000000050  0000000000000000   A       5     1     8
  [ 8] .rela.dyn         RELA             00000000000005e8  000005e8
       00000000000000c0  0000000000000018   A       4     0     8
  [ 9] .rela.plt         RELA             00000000000006a8  000006a8
       0000000000000048  0000000000000018  AI       4    24     8
  [10] .init             PROGBITS         0000000000001000  00001000
       000000000000001b  0000000000000000  AX       0     0     4
  [11] .plt              PROGBITS         0000000000001020  00001020
       0000000000000040  0000000000000010  AX       0     0     16
  [12] .text             PROGBITS         0000000000001060  00001060
       000000000000020b  0000000000000000  AX       0     0     16
  [13] .fini             PROGBITS         000000000000126c  0000126c
       000000000000000d  0000000000000000  AX       0     0     4
  [14] .rodata           PROGBITS         0000000000002000  00002000
       00000000000000cd  0000000000000000   A       0     0     8
  [15] .eh_frame_hdr     PROGBITS         00000000000020d0  000020d0
       0000000000000024  0000000000000000   A       0     0     4
  [16] .eh_frame         PROGBITS         00000000000020f8  000020f8
       000000000000007c  0000000000000000   A       0     0     8
  [17] .sframe           GNU_SFRAME       0000000000002178  00002178
       000000000000006c  0000000000000000   A       0     0     8
  [18] .note.gnu.pr[...] NOTE             0000000000002200  00002200
       0000000000000040  0000000000000000   A       0     0     8
  [19] .note.ABI-tag     NOTE             0000000000002240  00002240
       0000000000000020  0000000000000000   A       0     0     4
  [20] .init_array       INIT_ARRAY       0000000000003dd0  00002dd0
       0000000000000008  0000000000000008  WA       0     0     8
  [21] .fini_array       FINI_ARRAY       0000000000003dd8  00002dd8
       0000000000000008  0000000000000008  WA       0     0     8
  [22] .dynamic          DYNAMIC          0000000000003de0  00002de0
       00000000000001e0  0000000000000010  WA       5     0     8
  [23] .got              PROGBITS         0000000000003fc0  00002fc0
       0000000000000028  0000000000000008  WA       0     0     8
  [24] .got.plt          PROGBITS         0000000000003fe8  00002fe8
       0000000000000030  0000000000000008  WA       0     0     8
  [25] .data             PROGBITS         0000000000004018  00003018
       0000000000000010  0000000000000000  WA       0     0     8
  [26] .bss              NOBITS           0000000000004028  00003028
       0000000000000008  0000000000000000  WA       0     0     1
  [27] .comment          PROGBITS         0000000000000000  00003028
       000000000000001b  0000000000000001  MS       0     0     1
  [28] .shstrtab         STRTAB           0000000000000000  00003043
       000000000000010e  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  D (mbind), l (large), p (processor specific)
[amrit@amrit-pc C Folder]$ readelf -s hi

Symbol table '.dynsym' contains 9 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND 
     1: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _[...]@GLIBC_2.34 (2)
     2: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_deregisterT[...]
     3: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND __[...]@GLIBC_2.4 (3)
     4: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND [...]@GLIBC_2.2.5 (4)
     5: 0000000000000000     0 FUNC    GLOBAL DEFAULT  UND _[...]@GLIBC_2.38 (5)
     6: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND __gmon_start__
     7: 0000000000000000     0 NOTYPE  WEAK   DEFAULT  UND _ITM_registerTMC[...]
     8: 0000000000000000     0 FUNC    WEAK   DEFAULT  UND [...]@GLIBC_2.2.5 (4)
[amrit@amrit-pc C Folder]$ objdump -t hi

hi:     file format elf64-x86-64

SYMBOL TABLE:
no symbols


```

### Ghidra's Version of my main function 
```c
undefined8 FUN_00101159(void)

{
  long in_FS_OFFSET;
  char local_1d;
  uint local_1c;
  undefined8 local_18;
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  printf("Enter a character:");
  __isoc23_scanf(&DAT_0010201b,&local_1d);
  printf("Enter a integer:");
  __isoc23_scanf(&DAT_0010202f,&local_1c);
  printf("Enter a floating-point value:");
  __isoc23_scanf(&DAT_00102050,&local_18);
  printf("\nThe character you enterd is %c.\n",(ulong)(uint)(int)local_1d);
  printf("The integer you entered is %d.\n",(ulong)local_1c);
  printf("The floating-point value you enterd is %lf.\n",local_18);
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return 0;
}
```
The identified functions and their calls would be 
```c 
printf()
__isoc23_scanf()
```
As for the idenfitied strings it would be 
```c 
"Enter a character"
"Enter a integer:"
"Enter a floating-point value:"
"\nThe character you enterd is %c.\n"
"The integer you entered is %d.\n"
("The floating-point value you enterd is %lf.\n"
```
Ghidra has renamed some of the variables in this file with there being more variables then there was in the initate program.
```c 
long in_FS_OFFSET;
char local_1d;
uint local_1c;
undefined8 local_18;
long local_10;
```
For some bizzare reason, the local_10 variable iis assigned and has a weird if statement that doesn't make sense to me 
```c 
local_10 = *(long *)(in_FS_OFFSET + 0x28);
/*
I have no idea why it's assigned like this nor why
and also
*/ 
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
```
## Important commands in Assembly when it comes to reverse engineering 
Register: is a small, extremely fast storage location within the CPU that holds data, addresses, or instrucitons, serving as the primary interface for understanding binary behavior.
### Data Movement 
Mov: copies data from source to a destination. You see this constanly to load values into registers or memory
Push/pop: Places data onto the stack or removes it. These help you track function arguments and local variables
### Arithmetic and Logic
Add/Sub: Adds or subtract values. They reveal how loop counters or math formulas work.
And/ Or/Xor: Perform bitwise logic. XOR oftens zeros out a register or acts as a quck, basic encyption cipher
### Comparison and Testing
Cmp: compares two values by subtracting them and setting CPU flags. It precedes conditional jumps in if-statements
Test: Performs a bitwise AND without saving the result, updating flags.t It frequently checks if a register is zero (test EAX, EAX)
### Control Flow
JMP: Unconditionally jumps to a new memory address to redirect code execution
Conditional Jumps (JE,JNE,JG,JL): Jumps only if specific CPU flags are set from a prior comparison. These map directly to code logic like if,equals, or greater than.

Call/RET: Calls a subroutine or funciton and returns from it. They mark the boundaries of funcitons in a binary.
# Using GDB in order to step through the program
I first had to rerun the compiltation in order to add back the debug symbols which i didn't include the first time
```bash 
gdb ./hi_debug
```
After doing that in gdb I told it to break at main, so to pause at main then to run
```bash 
gbd) break main 
gbd) run
```
After that I ran through and did gdb list
```bash 
gdb) list
```
This was the contents of  it
```c
1       #include <stdio.h>  
2  
3       int main(void){  
4               char character;  
5               int integer;  
6               double float_point_value;  
7               printf("Enter a character:");  
8               scanf("%c",&character);  
9               printf("\nEnter a integer:");  
10              scanf("%d",&integer);
```
Then after doing that I then made sure to disassemble the main funciton
```bash 
gdb) dissable main
```

Which gave me this as its contents that it dumpled
```bash
Dump of assembler code for function main:  
  0x0000555555555159 <+0>:     push   %rbp  
  0x000055555555515a <+1>:     mov    %rsp,%rbp  
  0x000055555555515d <+4>:     sub    $0x20,%rsp  
=> 0x0000555555555161 <+8>:     mov    %fs:0x28,%rax  
  0x000055555555516a <+17>:    mov    %rax,-0x8(%rbp)  
  0x000055555555516e <+21>:    xor    %eax,%eax  
  0x0000555555555170 <+23>:    lea    0xe91(%rip),%rax        # 0x555555556008  
  0x0000555555555177 <+30>:    mov    %rax,%rdi  
  0x000055555555517a <+33>:    mov    $0x0,%eax  
  0x000055555555517f <+38>:    call   0x555555555040 <printf@plt>  
  0x0000555555555184 <+43>:    lea    -0x15(%rbp),%rax  
  0x0000555555555188 <+47>:    lea    0xe8c(%rip),%rdx        # 0x55555555601b  
  0x000055555555518f <+54>:    mov    %rax,%rsi  
  0x0000555555555192 <+57>:    mov    %rdx,%rdi  
  0x0000555555555195 <+60>:    mov    $0x0,%eax  
  0x000055555555519a <+65>:    call   0x555555555050 <__isoc23_scanf@plt>  
  0x000055555555519f <+70>:    lea    0xe78(%rip),%rax        # 0x55555555601e  
  0x00005555555551a6 <+77>:    mov    %rax,%rdi  
  0x00005555555551a9 <+80>:    mov    $0x0,%eax  
  0x00005555555551ae <+85>:    call   0x555555555040 <printf@plt>  
  0x00005555555551b3 <+90>:    lea    -0x14(%rbp),%rax  
  0x00005555555551b7 <+94>:    lea    0xe72(%rip),%rdx        # 0x555555556030  
  0x00005555555551be <+101>:   mov    %rax,%rsi  
  0x00005555555551c1 <+104>:   mov    %rdx,%rdi  
  0x00005555555551c4 <+107>:   mov    $0x0,%eax  
  0x00005555555551c9 <+112>:   call   0x555555555050 <__isoc23_scanf@plt>  
  0x00005555555551ce <+117>:   lea    0xe63(%rip),%rax        # 0x555555556038  
  0x00005555555551d5 <+124>:   mov    %rax,%rdi  
  0x00005555555551d8 <+127>:   mov    $0x0,%eax  
  0x00005555555551dd <+132>:   call   0x555555555040 <printf@plt>  
  0x00005555555551e2 <+137>:   lea    -0x10(%rbp),%rax  
  0x00005555555551e6 <+141>:   lea    0xe6a(%rip),%rdx        # 0x555555556057  
  0x00005555555551ed <+148>:   mov    %rax,%rsi  
  0x00005555555551f0 <+151>:   mov    %rdx,%rdi  
  0x00005555555551f3 <+154>:   mov    $0x0,%eax  
  0x00005555555551f8 <+159>:   call   0x555555555050 <__isoc23_scanf@plt>  
  0x00005555555551fd <+164>:   movzbl -0x15(%rbp),%eax  
  0x0000555555555201 <+168>:   movsbl %al,%eax  
  0x0000555555555204 <+171>:   lea    0xe55(%rip),%rdx        # 0x555555556060  
  0x000055555555520b <+178>:   mov    %eax,%esi  
  0x000055555555520d <+180>:   mov    %rdx,%rdi  
  0x0000555555555210 <+183>:   mov    $0x0,%eax  
  0x0000555555555215 <+188>:   call   0x555555555040 <printf@plt>  
  0x000055555555521a <+193>:   mov    -0x14(%rbp),%eax  
  0x000055555555521d <+196>:   lea    0xe64(%rip),%rdx        # 0x555555556088  
  0x0000555555555224 <+203>:   mov    %eax,%esi  
  0x0000555555555226 <+205>:   mov    %rdx,%rdi  
  0x0000555555555229 <+208>:   mov    $0x0,%eax  
  0x000055555555522e <+213>:   call   0x555555555040 <printf@plt>  
  0x0000555555555233 <+218>:   mov    -0x10(%rbp),%rax  
  0x0000555555555237 <+222>:   lea    0xe6a(%rip),%rdx        # 0x5555555560a8  
  0x000055555555523e <+229>:   movq   %rax,%xmm0  
  0x0000555555555243 <+234>:   mov    %rdx,%rdi  
  0x0000555555555246 <+237>:   mov    $0x1,%eax  
  0x000055555555524b <+242>:   call   0x555555555040 <printf@plt>  
  0x0000555555555250 <+247>:   mov    $0x0,%eax  
  0x0000555555555255 <+252>:   mov    -0x8(%rbp),%rdx  
  0x0000555555555259 <+256>:   sub    %fs:0x28,%rdx  
  0x0000555555555262 <+265>:   je     0x555555555269 <main+272>  
  0x0000555555555264 <+267>:   call   0x555555555030 <__stack_chk_fail@plt>  
  0x0000555555555269 <+272>:   leave  
  0x000055555555526a <+27
```
Then after that I got the info for each register by running this 
```bash 
gdb) info register
```

```bash 
rax            0x7ffff7e1dde8      140737352162792  
rbx            0x0                 0  
rcx            0x555555557dd8      93824992247256  
rdx            0x7fffffffe628      140737488348712  
rsi            0x7fffffffe618      140737488348696  
rdi            0x1                 1  
rbp            0x7fffffffe4e0      0x7fffffffe4e0  
rsp            0x7fffffffe4c0      0x7fffffffe4c0  
r8             0x7ffff7e16680      140737352132224  
r9             0x7ffff7e17fa0      140737352138656  
r10            0x7fffffffe240      140737488347712  
r11            0x7ffff7ffca90      140737354123920  
r12            0x7fffffffe618      140737488348696  
r13            0x1                 1  
r14            0x7ffff7ffd000      140737354125312  
r15            0x555555557dd8      93824992247256  
rip            0x555555555161      0x555555555161 <main+8>  
eflags         0x206               [ PF IF ]  
cs             0x33                51  
ss             0x2b                43  
ds             0x0                 0  
es             0x0                 0  
fs             0x0                 0  
gs             0x0                 0  
pl3_ssp        <unavailable>  
fs_base        0x7ffff7f8e740      140737353672512  
gs_base        0x0                 0  
(gdb) c
```
rip-instruction pointer, tells me " This is the instruciton the CPU is currently executing/about to execute"
rsp-This is the stack pointer, points to the current top of the stack
rbp- This is commonly used as a base/frame pointer for the current funciton
rax- this is commonly used for return values and other calculations 
Ran info frame
```bash 
gdb) info frame
Stack level 0, frame at 0x7fffffffe4f0:
 rip = 0x555555555161 in main (untitled.c:3); saved rip = 0x7ffff7c27781
 source language c.
 Arglist at 0x7fffffffe4e0, args: 
 Locals at 0x7fffffffe4e0, Previous frame's sp is 0x7fffffffe4f0
 Saved registers:
  rbp at 0x7fffffffe4e0, rip at 0x7fffffffe4e8

```
Now i can setp through the program one instruciton at a time.
```bash 
(gdb) si
0x000055555555516a      3       int main(void){
(gdb) si
0x000055555555516e      3       int main(void){
(gdb) si
7               printf("Enter a character:");
(gdb) si
0x0000555555555177      7               printf("Enter a character:");
(gdb) si
0x000055555555517a      7               printf("Enter a character:");
(gdb) si
0x000055555555517f      7               printf("Enter a character:");
(gdb) si
0x0000555555555040 in printf@plt ()
(gdb) si
0x0000555555555046 in printf@plt ()
(gdb) si
0x000055555555504b in printf@plt ()
(gdb) si
0x0000555555555020 in ?? ()
(gdb) si
0x0000555555555026 in ?? ()
(gdb) si
0x00007ffff7fd3fe0 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3fe4 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3fe5 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3fe8 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3fec in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3ff3 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3ff7 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd3ffc in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4001 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4006 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd400b in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4010 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4015 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd401a in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd401c in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4024 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd402c in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4034 in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd403c in ?? () from /lib64/ld-linux-x86-64.so.2
(gdb) si
0x00007ffff7fd4044 in ?? () from /lib64/ld-linux-x86-64.so.2

```
What the register looks like after running through some parts of the program
```bash
(gdb) info register
rax            0x800ee             524526
rbx            0x7fffffffe4a0      140737488348320
rcx            0x555555557dd8      93824992247256
rdx            0x0                 0
rsi            0x7fffffffe618      140737488348696
rdi            0x555555556008      93824992239624
rbp            0x7fffffffe4e0      0x7fffffffe4e0
rsp            0x7fffffffe0c0      0x7fffffffe0c0
r8             0x7ffff7e16680      140737352132224
r9             0x7ffff7e17fa0      140737352138656
r10            0x7fffffffe240      140737488347712
r11            0x7ffff7ffca90      140737354123920
r12            0x7fffffffe618      140737488348696
r13            0x1                 1
r14            0x7ffff7ffd000      140737354125312
r15            0x555555557dd8      93824992247256
rip            0x7ffff7fd4044      0x7ffff7fd4044
eflags         0x246               [ PF ZF IF ]
cs             0x33                51
ss             0x2b                43
ds             0x0                 0
es             0x0                 0
fs             0x0                 0
gs             0x0                 0
pl3_ssp        <unavailable>
fs_base        0x7ffff7f8e740      140737353672512
gs_base        0x0                 0
```
I just realized I stepped into the printf c library, so i redid it 

```bash 
Starting program: /home/amrit/Downloads/C Folder/hi_debug 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/usr/lib/libthread_db.so.1".

Breakpoint 1, main () at untitled.c:3
3       int main(void){
(gdb) break main
Note: breakpoint 1 also set at pc 0x555555555161.
Breakpoint 3 at 0x555555555161: file untitled.c, line 3.
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /home/amrit/Downloads/C Folder/hi_debug 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/usr/lib/libthread_db.so.1".

Breakpoint 1, main () at untitled.c:3
3       int main(void){
(gdb) disassemble main 
Dump of assembler code for function main:
   0x0000555555555159 <+0>:     push   %rbp
   0x000055555555515a <+1>:     mov    %rsp,%rbp
   0x000055555555515d <+4>:     sub    $0x20,%rsp
=> 0x0000555555555161 <+8>:     mov    %fs:0x28,%rax
   0x000055555555516a <+17>:    mov    %rax,-0x8(%rbp)
   0x000055555555516e <+21>:    xor    %eax,%eax
   0x0000555555555170 <+23>:    lea    0xe91(%rip),%rax        # 0x555555556008
   0x0000555555555177 <+30>:    mov    %rax,%rdi
   0x000055555555517a <+33>:    mov    $0x0,%eax
   0x000055555555517f <+38>:    call   0x555555555040 <printf@plt>
   0x0000555555555184 <+43>:    lea    -0x15(%rbp),%rax
   0x0000555555555188 <+47>:    lea    0xe8c(%rip),%rdx        # 0x55555555601b
   0x000055555555518f <+54>:    mov    %rax,%rsi
   0x0000555555555192 <+57>:    mov    %rdx,%rdi
   0x0000555555555195 <+60>:    mov    $0x0,%eax
   0x000055555555519a <+65>:    call   0x555555555050 <__isoc23_scanf@plt>
   0x000055555555519f <+70>:    lea    0xe78(%rip),%rax        # 0x55555555601e
   0x00005555555551a6 <+77>:    mov    %rax,%rdi
   0x00005555555551a9 <+80>:    mov    $0x0,%eax
   0x00005555555551ae <+85>:    call   0x555555555040 <printf@plt>
   0x00005555555551b3 <+90>:    lea    -0x14(%rbp),%rax
   0x00005555555551b7 <+94>:    lea    0xe72(%rip),%rdx        # 0x555555556030
   0x00005555555551be <+101>:   mov    %rax,%rsi
   0x00005555555551c1 <+104>:   mov    %rdx,%rdi
   0x00005555555551c4 <+107>:   mov    $0x0,%eax
   0x00005555555551c9 <+112>:   call   0x555555555050 <__isoc23_scanf@plt>
   0x00005555555551ce <+117>:   lea    0xe63(%rip),%rax        # 0x555555556038
   0x00005555555551d5 <+124>:   mov    %rax,%rdi
   0x00005555555551d8 <+127>:   mov    $0x0,%eax
   0x00005555555551dd <+132>:   call   0x555555555040 <printf@plt>
   0x00005555555551e2 <+137>:   lea    -0x10(%rbp),%rax
   0x00005555555551e6 <+141>:   lea    0xe6a(%rip),%rdx        # 0x555555556057
   0x00005555555551ed <+148>:   mov    %rax,%rsi
   0x00005555555551f0 <+151>:   mov    %rdx,%rdi
   0x00005555555551f3 <+154>:   mov    $0x0,%eax
   0x00005555555551f8 <+159>:   call   0x555555555050 <__isoc23_scanf@plt>
   0x00005555555551fd <+164>:   movzbl -0x15(%rbp),%eax
   0x0000555555555201 <+168>:   movsbl %al,%eax
   0x0000555555555204 <+171>:   lea    0xe55(%rip),%rdx        # 0x555555556060
   0x000055555555520b <+178>:   mov    %eax,%esi
   0x000055555555520d <+180>:   mov    %rdx,%rdi
   0x0000555555555210 <+183>:   mov    $0x0,%eax
   0x0000555555555215 <+188>:   call   0x555555555040 <printf@plt>
   0x000055555555521a <+193>:   mov    -0x14(%rbp),%eax
   0x000055555555521d <+196>:   lea    0xe64(%rip),%rdx        # 0x555555556088
   0x0000555555555224 <+203>:   mov    %eax,%esi
   0x0000555555555226 <+205>:   mov    %rdx,%rdi
   0x0000555555555229 <+208>:   mov    $0x0,%eax
   0x000055555555522e <+213>:   call   0x555555555040 <printf@plt>
   0x0000555555555233 <+218>:   mov    -0x10(%rbp),%rax
   0x0000555555555237 <+222>:   lea    0xe6a(%rip),%rdx        # 0x5555555560a8
   0x000055555555523e <+229>:   movq   %rax,%xmm0
   0x0000555555555243 <+234>:   mov    %rdx,%rdi
   0x0000555555555246 <+237>:   mov    $0x1,%eax
   0x000055555555524b <+242>:   call   0x555555555040 <printf@plt>
   0x0000555555555250 <+247>:   mov    $0x0,%eax
   0x0000555555555255 <+252>:   mov    -0x8(%rbp),%rdx
   0x0000555555555259 <+256>:   sub    %fs:0x28,%rdx
   0x0000555555555262 <+265>:   je     0x555555555269 <main+272>
   0x0000555555555264 <+267>:   call   0x555555555030 <__stack_chk_fail@plt>
   0x0000555555555269 <+272>:   leave
   0x000055555555526a <+273>:   ret
End of assembler dump.
(gdb) si
0x000055555555516a      3       int main(void){
(gdb) si
0x000055555555516e      3       int main(void){
(gdb) si
7               printf("Enter a character:");
(gdb) si
0x0000555555555177      7               printf("Enter a character:");
(gdb) si
0x000055555555517a      7               printf("Enter a character:");
(gdb) si
0x000055555555517f      7               printf("Enter a character:");
(gdb) nexti
8               scanf("%c",&character);
(gdb) si
0x0000555555555188      8               scanf("%c",&character);
(gdb) x/i $rip
=> 0x555555555188 <main+47>:    lea    0xe8c(%rip),%rdx        # 0x55555555601b
(gdb) 

```

I then proceeded to step through the things in the scanf and throughout the program
```bash 
(gdb) si 
0x000055555555518f      8               scanf("%c",&character);
(gdb) nexti
0x0000555555555192      8               scanf("%c",&character);
(gdb) si
0x0000555555555195      8               scanf("%c",&character);
(gdb) x/i $rip
=> 0x555555555195 <main+60>:    mov    $0x0,%eax
(gdb) si
0x000055555555519a      8               scanf("%c",&character);
(gdb) x/i $rip
=> 0x55555555519a <main+65>:    call   0x555555555050 <__isoc23_scanf@plt>
(gdb) info registers rdi rsi rdx
rdi            0x55555555601b      93824992239643
rsi            0x7fffffffe4cb      140737488348363
rdx            0x55555555601b      93824992239643
(gdb) x/s $rdi
0x55555555601b: "%c"
(gdb) 

```

```bash 
(gdb) x/s $rdi
0x55555555601b: "%c"
(gdb) p &character
$1 = 0x7fffffffe4cb ""
(gdb) nexti
Enter a character:h
9               printf("\nEnter a integer:");
(gdb) p character
$2 = 104 'h'
(gdb) 

```




```bash
                 Executable
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
       Ghidra                  GDB
     "What is this?"       "What is it doing?"
          │                     │
          ↓                     ↓
     Analyze/label          Run/debug
          │                     │
          ↓                     ↓
      main()              break main
      function A          step instruction
      function B          inspect registers
      string X             inspect stack
          │                     │
          └──────────┬──────────┘
                     ↓
              Understand program
```