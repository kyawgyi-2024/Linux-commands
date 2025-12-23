# Linux Day-9: Script Executable Permissions

🔹 Task Goal
Set proper permissions on a script (/tmp/xfusion.sh) to make it readable and executable for users.

🔹 Login to Application Server
ssh banner@stapp03                  # Login as user 'banner'

🔹 Switch to Root User (If Required)
sudo -i                             # Become root to modify permissions

🔹 Verify Current Permissions of Script
ls -lah /tmp/xfusion.sh             # Check current file permissions
# l → long listing format
# a → show hidden files (if any)
# h → human-readable sizes

🔹 Change Permissions to Readable and Executable
chmod +rx /tmp/xfusion.sh           # Add read and execute permissions
# chmod → command to change file permissions
# +r → add read permission
# +x → add execute permission
# /tmp/xfusion.sh → target script

✅ After this, users can read the script and run it as a program.

🔹 Verify Updated Permissions
ls -lah /tmp/xfusion.sh             # Confirm permissions are updated

# 📝 Summary
Logged into stapp03 as banner
Switched to root using sudo -i
Checked current permissions of /tmp/xfusion.sh
Added read and execute permissions using chmod +rx
Verified updated permissions

# 🎯 Interview Tips
chmod +rx <file> → common way to make scripts readable and executable
Always verify permissions with ls -l after changes
Understand symbolic (+r, +x) vs numeric (chmod 755) permissions
Executable scripts require x to be run, and r to be read