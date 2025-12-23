# Linux Day-8: Data Backup for Developer

🔹 Task Goal
Create a compressed backup of a developer’s data directory (/data/ammar), move it to the home directory, and verify its contents.

🔹 Login to Storage Server
ssh natasha@ststor01                 # Login as user 'natasha'

🔹 Switch to Root User (If Required)
sudo -i                              # Become root to ensure proper permissions

🔹 Create a Compressed Backup (tar.gz)
tar zcf ammar.tar.gz /data/ammar
# tar → archive utility
# z → compress using gzip
# c → create a new archive
# f → specify archive file name
# ammar.tar.gz → backup file name
# /data/ammar → directory to backup

🔹 Verify Backup File Exists
ls -l ammar.tar.gz                   # Check details of backup file
# Ensures backup was created with correct size and timestamp

🔹 Move Backup File to Home Directory
mv ammar.tar.gz /home/               # Move backup to /home/

🔹 Verify File in Home Directory
ls -l /home/ammar.tar.gz             # Confirm backup exists in home directory

🔹 List Contents of Backup File
tar -tf /home/ammar.tar.gz           # List files inside the tar.gz archive
# t → list contents
# f → specify archive file

# 📝 Summary
Logged into storage server ststor01
Switched to root using sudo -i
Created a compressed backup of /data/ammar → ammar.tar.gz
Moved backup to /home/ for easy access
Verified the archive and listed its contents

# 🎯 Interview Tips
tar zcf <archive>.tar.gz <directory> → standard Linux backup method
mv <file> <destination> → move files safely
tar -tf <archive> → quickly verify contents without extracting

Always check backup size and contents to avoid missing data