# Linux Day-6: Linux Data Transfer (User Files)

🔹 Task Goal
Count the number of files owned by a specific user (kareem) and copy all their files to a new location while preserving the directory structure.
# Source directory:
/home/usersdata/
# Destination directory:
/official/

🔹 Login to Target Server
ssh steve@stapp02                   # Login to application server

🔹 Switch to Root User (If Required)
sudo -i                              # Become root for permissions

🔹 Count Files Owned by User Kareem
find /home/usersdata/ -type f -user kareem | wc -l
# find → search directory
# -type f → only files
# -user kareem → files owned by 'kareem'
# wc -l → count number of files

🔹 Verify Destination Directory Exists
mkdir -p /official/                  # Create destination if not exists

🔹 Copy Files While Preserving Directory Structure
find /home/usersdata/ -type f -user kareem -exec cp --parents {} /official/ \;
# -exec cp → copy each found file
# --parents → preserve directory structure relative to /home/usersdata/
# {} → placeholder for found file
# /official/ → destination directory
# \; → end of -exec command

🔹 Optional: Faster Copy for Many Files Using xargs
find /home/usersdata/ -type f -user kareem -print0 | xargs -0 cp --parents -t /official/
# -print0 / -0 → safely handle filenames with spaces
# -t → target directory
# xargs → reduces number of cp executions for efficiency

# 📝 Summary

Logged in to stapp02 server as steve
Switched to root to ensure file access
Counted all files owned by kareem
Created destination /official/ if missing
Copied all files while preserving directory structure
Optional: used xargs for efficiency

# 🎯 Interview Tips
find / -type f -user <username> → locate all user files
cp --parents → preserves directory hierarchy
xargs -0 → handles large file sets and filenames with spaces
Always check destination path exists before copying