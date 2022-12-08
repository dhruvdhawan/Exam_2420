# Exam_2420
Part 1:

The apt update command will update the package lists to reflect the latest available versions of the software in the repositories. The apt upgrade command will then upgrade all of the installed packages to their latest versions.<pre><code>sudo apt update && sudo apt upgrade</pre></code>

Part 2:

Part 3:
<pre><code>journalctl -b -p warning -o json-pretty</pre></code>
I used
<pre><code>/-b</pre></code>
inside the man page to find boot option
<img src="images/1.png" width="800" />
Then I used
<pre><code>/-p</pre></code>
to find priority and then found the warning arugment
<img src="images/2.png" width="800" />
Finally I searched 
<pre><code>/pretty</pre></code>
<img src="images/3.png" width="800" />
and found output field command

Part 4:
<pre><code>#!/bin/bash
#!/bin/bash

# Find all users with a UID between 1000 and 5000
users=$(awk -F: '$3 >= 1000 && $3 <= 5000 {print $1}' /etc/passwd)

# Get the current user
current_user=$(whoami)

# Create the message to write to the /etc/motd file
message="Regular users:\n"
for user in $users; do
  shell=$(grep "^$user:" /etc/passwd | cut -d: -f7)
  uid=$(grep "^$user:" /etc/passwd | cut -d: -f3)
  message="$message - $user (UID: $uid): $shell\n"
done
message="$message\nCurrently logged in user: $current_user"

# Write the message to the /etc/motd file
echo -e "$message" > /etc/motd

</pre></code>

Part 5:
<pre><code>
[Unit]
Description=Run my script from Part 4
[Service]
Type=simple
ExecStart=/bin/bash /scripts/find_users.sh

[Install]
WantedBy=multi-user.target
</pre></code>
Part 6:
Timer Unit file
File Path: /etc/systemd/system/motd.timer
<pre><code>
[Unit]
Description=Run motd.service one minute after boot and every day thereafter

[Timer]
OnBootSec=1min
OnUnitActiveSec=1day

[Install]
WantedBy=timers.target
EO
</pre></code>






