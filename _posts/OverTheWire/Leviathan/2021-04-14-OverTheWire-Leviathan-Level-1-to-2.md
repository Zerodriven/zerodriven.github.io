---
layout: post
date:   2021-04-17 10:20:00 +0100
categories: OverTheWire Leviathan
---


# Leviathan 1
```

Username: leviathan1
Password: rioGegei8m

Data for the levels can be found in **the homedirectories**. You can look at **/etc/leviathan\_pass** for the various level passwords.
```


## Lets take a look

```bash
leviathan1@leviathan:~$ ls
check
leviathan1@leviathan:~$ file ./check
./check: setuid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.32, BuildID[sha1]=c735f6f3a3a94adcad8407cc0fda40496fd765dd, not stripped
```

## Okay, lets run this..

```bash
leviathan1@leviathan:~$ ./check
password: hello
Wrong password, Good Bye ...
```

## Okay, what did we learn from Rabit? Lets check some strings

```bash
leviathan1@leviathan:~$ strings ./check
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
puts
setreuid
printf
getchar
system
geteuid
strcmp
__libc_start_main
__gmon_start__
GLIBC_2.0
PTRhp
QVh;
secrf
love
UWVS
t$,U
[^_]
password:
/bin/sh
Wrong password, Good Bye ...
;*2$"
GCC: (Debian 6.3.0-18+deb9u1) 6.3.0 20170516
crtstuff.c
__JCR_LIST__
deregister_tm_clones
__do_global_dtors_aux
completed.6587
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
check.c
__FRAME_END__
__JCR_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
strcmp@@GLIBC_2.0
__x86.get_pc_thunk.bx
printf@@GLIBC_2.0
getchar@@GLIBC_2.0
_edata
geteuid@@GLIBC_2.0
__data_start
puts@@GLIBC_2.0
system@@GLIBC_2.0
__gmon_start__
__dso_handle
_IO_stdin_used
setreuid@@GLIBC_2.0
__libc_start_main@@GLIBC_2.0
__libc_csu_init
_fp_hw
__bss_start
main
__TMC_END__
.symtab
.strtab
.shstrtab
.interp
.note.ABI-tag
.note.gnu.build-id
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rel.dyn
.rel.plt
.init
.plt.got
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.jcr
.dynamic
.got.plt
.data
.bss
.comment
```

## Love? What does love do?

```bash
leviathan1@leviathan:~$ ./check
password: love
Wrong password, Good Bye ...
```

## Nothing. -An eternity later- I discoverd ltrace.

```bash
leviathan1@leviathan:~$ ltrace ./check
__libc_start_main(0x804853b, 1, 0xffffd794, 0x8048610 <unfinished ...>
printf("password: ")                                                      = 10
getchar(1, 0, 0x65766f6c, 0x646f6700password: hello
)                                     = 104
getchar(1, 0, 0x65766f6c, 0x646f6700)                                     = 101
getchar(1, 0, 0x65766f6c, 0x646f6700)                                     = 108
strcmp("hel", "sex")                                                      = -1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)                                      = 29
+++ exited (status 0) +++
```

## So.. Sex. Love, Secret and Sex. Did Hackers teach me nothing?

```bash
leviathan1@leviathan:~$ ./check
password: sex
$
$ cat ../../etc/leviathan_pass/leviathan2
ougahZi8Ta
```

VICTORY.

```
ougahZi8Ta 
```
