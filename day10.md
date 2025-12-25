# 🐧 Linux-10: File Permission Correction (Using ACL)

🔹 Task Goal
Fix file permissions on /etc/hostname using Access Control Lists (ACL) so that:
User koko → no permissions
User moemoe → read-only permission
Target file:
/etc/hostname

🔹 Login to Application Server
ssh tony@stapp01                    # Login to application server as user 'tony'

🔹 Switch to Root User
sudo -i                             # Become root (required to modify /etc files)

🔹 Check Current File Permissions
ls -l /etc/hostname                # View owner, group, and basic permissions
# -l → long listing format
# Shows rwx permissions for owner, group, and others

🔹 View Current ACL Rules
getfacl /etc/hostname              # Display existing ACL entries
# getfacl → shows Access Control List details
# Useful to confirm no custom user permissions exist yet

🔹 Remove All Permissions for User koko
setfacl -m u:koko:--- /etc/hostname
# setfacl → command to modify ACL
# -m → modify ACL entry
# u:koko → user 'koko'
# --- → no read, write, or execute permission
# /etc/hostname → target file

🔹 Grant Read-Only Permission to User moemoe
setfacl -m u:moemoe:r-- /etc/hostname
# u:moemoe → user 'moemoe'
# r-- → read-only permission
# User can read the file but cannot modify it

🔹 Verify Updated ACL Permissions
getfacl /etc/hostname              # Confirm ACL changes are applied
# Should show:
# user:koko:---
# user:moemoe:r--

# 📝 Summary
Logged into stapp01 as tony
Switched to root using sudo -i
Checked default permissions of /etc/hostname
Removed all permissions for user koko using setfacl
Granted read-only access to user moemoe
Verified ACL configuration with getfacl

# 🎯 Interview Tips
setfacl -m u:<user>:<perm> <file> → set user-specific permissions
ACL works in addition to chmod permissions
getfacl is always used to verify ACL changes
Common in enterprise Linux & DevOps environments