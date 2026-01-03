# Q1.
As part of the temporary resource allocation, Ammar has been appointed to the Nautilus project as a backup developer. To facilitate this, a temporary user account is required for Ammar. It is advisable to create a user account with a specified expiration date to ensure restricted server access beyond the designated period.
A user profile under the name ammar has already been established on App Server 2 within the Stratos Datacenter. Adjust the account's expiration date to 2024-02-17. Additionally, locate all files (excluding directories) owned by this user within the /home/usersdata directory and copy them to the /official directory while maintaining their original ownership.
-------------------------------------------------------------------------------------------------
Here’s how to complete the task safely and correctly on App Server 2.
# 1️⃣ Set account expiration date for user ammar
---
sudo chage -E 2024-02-17 ammar
---
(Use chage to modify the account expiry date.)
✅ Verify the change:
sudo chage -l ammar
You should see:
Account expires : Feb 17, 2024

# 2️⃣ Find all files owned by ammar in /home/usersdata (exclude directories)
---
find /home/usersdata -type f -user ammar
---
We’ll use find:
-type f → files only
-user ammar → owned by ammar

# 3️⃣ Copy those files to /official while preserving ownership
---
sudo find /home/usersdata -type f -user ammar -exec cp -p {} /official/ \;
---
To keep the original owner and group, use cp -p (or -a).
Why this works:
cp -p → preserves ownership, permissions, timestamps
-exec ... \; → copies each file found
Directories are excluded because of -type f

# 4️⃣ Verify ownership in /official
---
ls -l /official
---
You should see files still owned by:
ammar ammar
✅ Summary
✔ User ammar account expiration set to 2024-02-17
✔ All files only (no directories) copied from /home/usersdata
✔ Ownership preserved in /official
If you want, I can also provide a one-liner validation command to double-check everything at once 👍

==================================================================================================
# Q2.
One of the developers at Nautilus has stored sensitive data on the jump host in Stratos DC. This data needs to be transferred to an app server. As developers lack access to the app servers, they've requested the system admin team to complete this task.
Please copy the file /tmp/nautilus.txt.gpg from the jump server to App Server 2 at the following location: /home/nfsshare.
--------------------------------------------------------------------------------------------------
This is a straightforward secure copy (scp) task performed by the system admin from the jump host to App Server 2.
✅ Task Summary
Source (Jump Server): /tmp/nautilus.txt.gpg
Destination (App Server 2): /home/nfsshare
File type: Encrypted (.gpg) – no decryption required

# 1️⃣ Log in to the Jump Host
ssh thor@jump_host

# 2️⃣ Copy the file to App Server 2
scp /tmp/nautilus.txt.gpg thor@app02:/home/nfsshare/

Use scp to securely transfer the file:
📌 Notes:
thor → default admin user (adjust if different)
app02 → hostname of App Server 2
Trailing / ensures it’s copied into the directory

# 3️⃣ Verify on App Server 2
ssh thor@app02
ls -l /home/nfsshare

You should see:
nautilus.txt.gpg
✅ Final Result
✔ File securely copied from Jump Host
✔ File placed in /home/nfsshare on App Server 2
✔ No permission or ownership issues

=================================================================================================
# Q3.
One user needs to be created on an app server in Stratos Datacenter. The system admins team has shared more details below regarding the same.
a. The user name should be rajesh on App server 2 in Stratos Datacenter.
b. Set its UID to 1717 and home directory to /opt/rajesh (you can create this directory if it doesn't exist).
c. Also create a group named nautilus_sftp_users on App server 2 in Stratos Datacenter. Add the user rajesh to the nautilus_sftp_users group.
-------------------------------------------------------------------------------------------------

# 1️⃣ Log in to App Server 2
ssh thor@app02

# 2️⃣ Create the group nautilus_sftp_users
sudo groupadd nautilus_sftp_users

✅ Verify:
getent group nautilus_sftp_users

# 3️⃣ Create the user rajesh with required UID and home directory
sudo useradd -u 1717 -d /opt/rajesh -m -g nautilus_sftp_users rajesh

Explanation:
-u 1717 → sets UID
-d /opt/rajesh → custom home directory
-m → creates the home directory if it doesn’t exist
-g nautilus_sftp_users → primary group

# 4️⃣ Verify user and group configuration - Check user details:
id rajesh

Expected output:
uid=1717(rajesh) gid=XXXX(nautilus_sftp_users) groups=nautilus_sftp_users
Check home directory:
---
ls -ld /opt/rajesh
---
Expected:
drwx------ rajesh nautilus_sftp_users /opt/rajesh
✅ Final Checklist
✔ User rajesh created
✔ UID set to 1717
✔ Home directory /opt/rajesh created
✔ Group nautilus_sftp_users created
✔ User added to the group

=================================================================================================
# Q4.
The Nautilus security team performed an audit on all servers present in Stratos DC. During the audit some critical data/files were identified which were having the wrong permissions as per security standards. Once the report was shared with the production support team, they started fixing the issues one by one. It has been identified that one of the files named /etc/hosts on Nautilus App 2 server has wrong permissions, so that needs to be fixed and the correct ACLs needs to be applied.
a. User virat must not have any permission on this file.
b. User vivek should have read only permission on this file. Further, sysops group should have read/write permissions on this file.

# 1️⃣ Log in to App Server 2
ssh thor@app02

# 2️⃣ Ensure ACL support is available
(Usually already enabled, but safe to check)
mount | grep ' /etc '

If ACLs weren’t supported, setfacl would fail—but in Stratos labs, ACLs are enabled.

# 3️⃣ Remove all permissions for user virat
sudo setfacl -x u:virat /etc/hosts

This guarantees no access at all for virat.

# 4️⃣ Grant read-only permission to user vivek
sudo setfacl -m u:vivek:r /etc/hosts

# 5️⃣ Grant read/write permission to group sysops
sudo setfacl -m g:sysops:rw /etc/hosts

# 6️⃣ Verify ACLs
getfacl /etc/hosts

Expected relevant output:
user:vivek:r--
group:sysops:rw-
❌ No entry for virat (or explicitly user:virat:---)

✅ Final Result
✔ virat → no permissions
✔ vivek → read-only
✔ sysops group → read & write
✔ Security audit requirement satisfied

==================================================================================================
# Q5.
To test a newly installed web server, we need to create an index.html file on an app server in Stratos Datacenter. You can find more details below about this task:
Create a file named index.html under /var/www/html directory on App server 2. Add below line in this file:“nginx web server”
Create /var/www/html/index.html
-------------------------------------------------------------------------------------------------

# 1️⃣ Log in to App Server 2
ssh thor@app02

# 2️⃣ Create index.html with the required content
Use echo to create the file and add the line nginx web server:
---
sudo echo "nginx web server" > /var/www/html/index.html
---
✅ This will:
Create the file if it doesn’t exist
Overwrite it if it already exists
Add exactly the required line

# 3️⃣ Verify the file content
cat /var/www/html/index.html

Expected output:nginx web server

# 4️⃣ (Optional) Check file permissions
ls -l /var/www/html/index.html

Typical permissions:
-rw-r--r-- 1 root root
✅ Final Result
✔ index.html created at /var/www/html
✔ Content added: nginx web server
✔ Ready to test the web server

==================================================================================================
# Q6.
The development team requires specific logs stored within the Nautilus storage server situated in the Stratos DC. Access the designated location on the server to retrieve the necessary logs. Further, perform below actions:
Create a tar archive named logs.tar (under natasha's home) of /var/log/ directory.
Now, create a compressed tar archive as well named logs.tar.gz (under natasha's home) of /var/log/ directory.
-------------------------------------------------------------------------------------------------

# 1️⃣ Log in to the storage server
ssh natasha@ststor01

# 2️⃣ Go to natasha’s home directory
cd /home/natasha

# 3️⃣ Create an uncompressed tar archive logs.tar
tar -cvf logs.tar /var/log

Explanation:
c → create archive
v → verbose (shows files being added)
f → file name (logs.tar)

# 4️⃣ Create a compressed tar archive logs.tar.gz
tar -czvf logs.tar.gz /var/log

Additional flag:
z → gzip compression

# 5️⃣ Verify the archives
ls -lh /home/natasha/logs.tar /home/natasha/logs.tar.gz

You should see both files present.
✅ Final Checklist
✔ logs.tar created under /home/natasha
✔ logs.tar.gz created under /home/natasha
✔ Both archives contain /var/log directory

=================================================================================================
# Q7.
There is some data on Nautilus App Server 2 in Stratos DC. Data needs to be altered in some of the files. On Nautilus App Server 2, alter the /home/BSD.txt file as per details given below.
a. Delete all lines containing the word code and save the results in /home/BSD_DELETE.txt file. (Please be aware of case sensitivity)
b. Replace all occurrences of the word the (look for the exact match) with them and save the results in /home/BSD_REPLACE.txt file.
Note: Let's say you are asked to replace the word to with from. In that case, make sure not to alter any words containing the string itself, for example; upto, contributor etc.
-------------------------------------------------------------------------------------------------

# 1️⃣ Log in to App Server 2
ssh thor@app02

# 2️⃣ Task (a): Delete lines containing the word code (case-sensitive)
We will remove entire lines that contain code and save the output to a new file.
---
grep -v "code" /home/BSD.txt > /home/BSD_DELETE.txt
---
✔ What this does
grep -v → excludes matching lines
"code" → case-sensitive match (CODE / Code will NOT be removed)
Output saved to /home/BSD_DELETE.txt

# 3️⃣ Task (b): Replace exact word the with them
We must replace only the exact word, not parts of other words.
---
sed 's/\bthe\b/them/g' /home/BSD.txt > /home/BSD_REPLACE.txt
---
✔ Why this is correct
\b → word boundary
Ensures:
✅ the → them
❌ there, other, themself remain unchanged

# 4️⃣ Verify the results
cat /home/BSD_DELETE.txt
cat /home/BSD_REPLACE.txt

(Optional comparison)
diff /home/BSD.txt /home/BSD_REPLACE.txt

✅ Final Result
✔ Lines containing code removed → BSD_DELETE.txt
✔ Exact word the replaced with them → BSD_REPLACE.txt
✔ Original file remains unchanged

===================================================================================================
# Q8.
On our Storage server in Stratos Datacenter we are having some issues where the nfsuser user is holding hundreds of processes, which is degrading the performance of the server. Therefore, we have a requirement to limit its maximum processes. Please set its maximum process limits as below:

a. soft limit = 1026
b. hard_limit = 2027
-------------------------------------------------------------------------------------------------

# 1️⃣ Log in to the Storage Server
ssh thor@ststor01

# 2️⃣ Edit the limits configuration file
Open /etc/security/limits.conf:
---
sudo vi /etc/security/limits.conf
---

# 3️⃣ Add process limits for user nfsuser
At the end of the file, add the following lines:
-----
nfsuser  soft  nproc  1026
nfsuser  hard  nproc  2027
-----
Explanation:
nfsuser → target user
soft nproc 1026 → soft process limit
hard nproc 2027 → hard process limit

Save and exit->Press ESC->Type :wq->Press Enter

# 5️⃣ Verify (after re-login)
The limits take effect after the user logs in again.
Switch to nfsuser or log in as that user:
---
su - nfsuser
---
Check limits:
---
ulimit -u
---
Expected output:1026

To view hard limit:
---
ulimit -Hu
---
Expected output:2027

✅ Final Result
✔ Soft process limit set to 1026
✔ Hard process limit set to 2027
✔ Server performance protected from process exhaustion
==================================================================================================

# Q9.
Some new requirements have been shared by the Nautilus application development team, a new package need to be installed on all app servers in Stratos Datacenter.
Install the bind package on all app servers in Stratos Datacenter and start/enable its service.
-------------------------------------------------------------------------------------------------
To meet this requirement, perform the following steps on ALL App Servers in Stratos Datacenter (for example: app01, app02, app03).

# 1️⃣ Log in to each App Server
ssh thor@app01

# 2️⃣ Install the bind package
On RHEL / CentOS / Rocky / AlmaLinux:
---
sudo yum install -y bind
---
(If the system uses dnf, this command still works.)

# 3️⃣ Start the BIND service
The service name for bind is named.
---
sudo systemctl start named
---
Enable the service at boot
---
sudo systemctl enable named
---
Verify service status
---
sudo systemctl status named
---
You should see:
Active: active (running)
# Repeat on all app servers
(Repeat the same steps on app02, app03, etc.)

✅ Final Checklist
✔ bind package installed on all app servers
✔ named service started
✔ named service enabled at boot
=================================================================================================
# Q10.
As per a new application requirements shared by the Nautilus application development team, several new packages need to be installed on all app servers in Stratos Datacenter. Most of them are installed except samba.
Therefore, install the samba package on all app servers in Stratos Datacenter.
------------------------------------------------------------------------------------------------

# 1️⃣ Log in to each App Server
ssh thor@app01

# 2️⃣ Install the samba package
On RHEL / CentOS / Rocky / AlmaLinux:
---
sudo yum install -y samba
---
Or, if the system uses dnf:
sudo dnf install -y samba

# 3️⃣ Verify installation
---
rpm -q samba
---
Expected output (example):
samba-4.16.5-0.el8.x86_64

# 4️⃣ (Optional) Enable and start Samba services
If the application requires the Samba services to be running:
sudo systemctl start smb
sudo systemctl enable smb
sudo systemctl start nmb
sudo systemctl enable nmb

Verify:
---
sudo systemctl status smb nmb
---

# 5️⃣ Repeat on all App Servers
Run steps 1–4 on every app server in Stratos DC.
(Repeat on app02, app03, etc.)

✅ Final Checklist
✔ samba package installed on all app servers
✔ (Optional) Samba services running and enabled
==================================================================================================