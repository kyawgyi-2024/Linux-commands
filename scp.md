# 🐧 Linux: Stop FTP – Secure File Transfer Using SCP

🔹 Task Goal
Transfer an encrypted file without using FTP, using SCP (Secure Copy) as the only allowed method to copy files between Linux servers.
---
Source file:
/tmp/nautilus.txt.gpg
---
Destination server & path:
banner@stapp03:/home/app

🔹 Verify File on Source Server
ls -l /tmp/nautilus.txt.gpg          # Confirm the file exists and check permissions
# -l → long listing format
# Shows file size, owner, group, and permission bits
# Ensures the source file is ready for transfer

🔹 Transfer File Using SCP
scp /tmp/nautilus.txt.gpg banner@stapp03:/home/app
# scp → secure copy command (SSH-based)
# /tmp/nautilus.txt.gpg → source file path
# banner@stapp03 → destination user and server
# :/home/app → destination directory on remote server
# You will be prompted for banner's password
✅ File is securely transferred using SSH encryption
❌ No FTP service is used

🔹 Login to Destination Server
ssh banner@stapp03                  # Login to destination server

🔹 Verify File on Destination
ls -l /home/app                     # Confirm file was copied successfully
# Should display nautilus.txt.gpg in the directory
# Verifies ownership and permissions after transfer

# 📝 Summary
Verified encrypted file exists on source server
Transferred file using scp (FTP not used)
Authenticated using banner's password
Logged into destination server
Confirmed file exists in /home/app

# 🎯 Interview Tips
scp uses SSH → encrypted & secure
Syntax:
scp <source> <user>@<host>:<destination>
SCP is commonly used when:
FTP is disabled
Secure transfers are required
Quick, one-time file copies are needed
For directories:
scp -r <dir> user@host:/path

✔ Frequently asked in Linux Admin & DevOps interviews
