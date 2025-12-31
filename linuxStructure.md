# 📁 Linux Root Directory Structure (/)

Everything in Linux starts from root /.
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── username
├── lib
├── lib64
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
│   ├── bin
│   ├── lib
│   ├── local
│   └── sbin
└── var
    ├── log
    ├── tmp
    └── www

🧠 Important Directories (Simple Explanation)
# /bin  → basic commands
Essential commands;
Example: ls, cp, mv, cat
Needed for system to work

# /boot → Bootloader & kernel files
Example: vmlinuz, grub
Don’t touch unless you know what you’re doing

# /dev  → Device files
Example:
/dev/sda → hard disk
/dev/tty → terminal

# /etc  → Configuration files
Example:
/etc/passwd
/etc/nginx/nginx.conf
📌 No program binaries here

# /home → Normal users’ home folders
Example:
/home/kyawmoe
├── Documents
├── Downloads
├── Desktop

# /lib & /lib64
Shared libraries for system programs
Similar to .dll in Windows

# /media
Automatically mounted devices
USB, CD, external drives

# /mnt
Temporary manual mounts
Example: mounting a disk for testing

# /opt  → Optional / third-party software
Example:
/opt/google
/opt/vscode

# /proc
Virtual filesystem
System & process info (CPU, memory)
Files are generated automatically

# /root
Home directory for root user
Not the same as /

# /run
Runtime data
PID files, sockets

# /sbin
System admin commands
Example: reboot, iptables

# /srv
Service data
Web, FTP, etc.

# /sys
Kernel & hardware information
Advanced usage

# /tmp
Temporary files
Auto-deleted after reboot

# /usr
User-installed programs
Main software directory
/usr/bin     → user commands
/usr/lib     → libraries
/usr/local   → manually installed apps

# /var
Variable data (changes often)
/var/log     → logs
/var/tmp     → temp files
/var/www     → website files

# 📄 Common Linux File Types
Type	Meaning
-	Regular file
d	Directory
l	Symbolic link
c	Character device
b	Block device
📝 Tip for Your Learning Notes

# You can write like this in your notebook:
/bin  → basic commands
/etc  → config files
/home → user data
/var  → logs & variable files

-------------------------------------------------------------------------------------------