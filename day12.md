# 🐧 Linux Day-12: Secure Data Transfer (Using SCP)

🔹 Task Goal
Securely transfer an encrypted file from the local server to an application server using SCP (Secure Copy).
Source file:/tmp/nautilus.txt.gpg

Destination server & path:
tony@stapp01:/home/nfsdata

🔹 Verify Source File Location
cd /tmp ; ls                         # Navigate to /tmp and list files
# cd /tmp → move to temporary directory
# ls → confirm nautilus.txt.gpg exists

🔹 Return to Home Directory
cd ~                                 # Go back to user's home directory
# ~ → shortcut for current user's home

🔹 Transfer File Securely Using SCP : scp <source> <user>@<host>:<destination>
scp /tmp/nautilus.txt.gpg tony@stapp01:/home/nfsdata
# scp → secure copy over SSH
# /tmp/nautilus.txt.gpg → source file
# tony@stapp01 → destination user and server
# :/home/nfsdata → destination directory
# You will be prompted for tony's password
✅ File is transferred securely using SSH encryption
❌ No FTP or insecure protocol is used

🔹 Verify File on Destination Server
cd /home/nfsdata ; ls                # Navigate and list destination directory
# Confirms nautilus.txt.gpg was copied successfully

# 📝 Summary
Verified encrypted file exists in /tmp
Returned to home directory
Transferred file securely using scp
Authenticated with tony's password
Checked destination directory for file

# 🎯 Interview Tips
scp uses SSH → encrypted data transfer
Syntax:
scp <source> <user>@<host>:<destination>

Commonly used for:
Secure file copy between servers
Environments where FTP is disabled
Use -r flag to copy directories:
scp -r /dir user@host:/path

✔ Frequently asked in Linux Admin & DevOps interviews