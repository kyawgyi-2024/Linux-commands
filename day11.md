# 🐧 Linux Day-11: String Replacement (XML File Maintenance)

🔹 Task Goal
Update a template XML file on the backup server by replacing all occurrences of a specific string.
Required change:
Replace Random ➜ Marine
Target file: /root/nautilus.xml
Server:stbkp01

🔹 Login to Backup Server
ssh clint@stbkp01                   # Login to backup server as user 'clint'

🔹 View Current XML File Content
sudo cat /root/nautilus.xml         # Display the XML file content
# sudo → required because file is owned by root
# cat → prints file content to the terminal
# Used to confirm existing occurrences of the string "Random"

🔹 Open XML File for Editing
sudo vi /root/nautilus.xml          # Open the XML file in vi editor
# vi → text editor commonly used in Linux servers

🔹 Replace All Occurrences of the String
Inside vi, run:
:%s/Random/Marine/g

Explanation ; 
:        → command mode
%        → apply to entire file
s        → substitute command
Random   → string to be replaced
Marine   → replacement string
g        → global (replace all occurrences on every line)

Expected output: (66 substitutions on 66 lines)
Confirms all instances were successfully replaced

🔹 Save and Exit the File
:x
Explanation:
:x → save changes and exit vi (same as :wq)

# 📝 Summary
Logged into stbkp01 as clint
Viewed existing XML file content
Opened /root/nautilus.xml in vi
Replaced all occurrences of "Random" with "Marine"
Verified 66 substitutions were made
Saved changes and exited editor

# 🎯 Interview Tips
:%s/old/new/g → replace string in entire file
:s/old/new/ → replace first occurrence in current line only

Always verify substitutions count in vi
String replacement is common in:
Configuration files
XML/JSON templates
DevOps automation tasks

✔ Very common KodeKloud Linux & DevOps challenge
