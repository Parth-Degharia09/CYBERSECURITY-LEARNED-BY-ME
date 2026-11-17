Day 04 – OverTheWire Bandit (Level 13–18)

Level 13–14

Task

The password for the next level is stored in "/etc/bandit_pass/bandit14" and can only be read by user "bandit14".

For this level, instead of receiving the next password, we are provided with a private SSH key that can be used to log in to the next level.

Steps Performed

1. Listed all files, including hidden files:
   
   ls -la

2. Displayed the private SSH key:
   
   cat sshkey.private

3. Checked the current working directory:
   
   pwd

4. Exited the remote Bandit server:
   
   exit

5. From my local machine, copied the private SSH key using "scp":
   
   scp -P 2220 bandit13@bandit.labs.overthewire.org:/home/bandit13/sshkey.private .

6. Entered the password for Bandit 13 when prompted.

7. Changed the permissions of the private key:
   
   chmod 600 sshkey.private

8. Used the private SSH key to log in as Bandit 14:
   
   ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org

9. Retrieved the password:
   
   cat /etc/bandit_pass/bandit14

Problem Faced

The "scp" command was completely new to me, so I initially panicked because I was unfamiliar with its syntax and usage.

After researching, I understood the different parts of the command:

- "scp" – Securely copies files between local and remote systems.
- "-P 2220" – Specifies the SSH port. Here, "-P" is uppercase.
- "bandit13@bandit.labs.overthewire.org" – Specifies the remote username and server.
- "/home/bandit13/sshkey.private" – Specifies the location and name of the private key on the remote server.
- "." – Copies the file into the current local directory.
- "chmod 600" – Gives the file owner read and write permissions while removing permissions for other users.
- "ssh -i" – Uses the specified private key for authentication instead of entering a password.

After understanding these commands, I successfully logged in to Bandit 14 using the private SSH key.

---

Level 14–15

Task

The password for the next level can be retrieved by submitting the password of the current level to port "30000" on localhost.

Steps Performed

1. Listed the files:
   
   ls -la

2. Connected to port 30000 using Netcat:
   
   nc localhost 30000

3. Pasted the current level's password into the connection.

4. Received the password for the next level.

Problem Faced

Initially, I was unfamiliar with the "nc" command. After researching, I learned that Netcat (or "nc") is a networking utility used for communicating over TCP and UDP connections.

I also learned that it can be used to connect to specific ports and exchange data with services running on those ports.

- "nc" – Netcat networking utility.
- "localhost" – Refers to the current machine.
- "30000" – The port to which the connection is established.

After understanding how Netcat works, I submitted the current password and retrieved the next one.

---

Level 15–16

Task

The password for the next level can be retrieved by submitting the password of the current level to port "30001" on localhost using SSL/TLS encryption.

Steps Performed

1. Listed the files:
   
   ls -la

2. Established an SSL/TLS connection using OpenSSL:
   
   openssl s_client -connect localhost:30001

3. Pasted the previous level's password into the connection.

4. Received the password for the next level.

Problem Faced

Since I am still fairly new to Linux and learning commands bit by bit, I was unfamiliar with OpenSSL.

After researching, I understood the purpose of the command:

- "openssl" – A command-line tool used for cryptographic operations.
- "s_client" – Starts an SSL/TLS client connection.
- "-connect localhost:30001" – Connects to port 30001 on the local machine.

It took me a few attempts to get everything right, but after understanding how the connection worked, I successfully retrieved the password.

---

Level 16–17

Task

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range "31000" to "32000".

First, we need to identify which ports have a server listening on them. Then, we need to determine which servers support SSL/TLS encryption.

Only one server will provide the next credentials, while the others will simply return whatever data we send to them.

Steps Performed

1. Listed the files:
   
   ls -la

2. Scanned the specified port range using Nmap:
   
   nmap -p 31000-32000 localhost

3. Tested the available ports using Netcat:
   
   nc localhost <port>
   
   Many ports simply returned the same data that I sent. I identified the ports that behaved differently for further testing.

4. Tested the candidate ports for SSL/TLS support:
   
   openssl s_client -connect localhost:<port>

5. Submitted the current level's password to the correct SSL/TLS service:
   
   cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:<port> -quiet

6. Received the private SSH key for Bandit 17.

7. Exited the connection:
   
   exit

8. Copied the private SSH key from the terminal output and saved it on my local machine.

9. Created a file to store the private key:
   
   touch sshkey.private

10. Opened the file using Nano:
    
    nano sshkey.private

11. Pasted the private SSH key into the file.

12. Saved and exited Nano:
    
    - "Ctrl + O" – Save the file.
    - "Enter" – Confirm the filename.
    - "Ctrl + X" – Exit Nano.

13. Changed the private key permissions:
    
    chmod 600 sshkey.private

14. Logged in to Bandit 17 using the private SSH key:
    
    ssh -i sshkey.private -p 2220 bandit17@bandit.labs.overthewire.org

Problem Faced

The biggest difficulty I faced in this level was handling the SSH private key.

Some online tutorials suggested that I could log in directly from inside Bandit 16 to Bandit 17. However, that approach did not work in my case.

I had to copy the private SSH key to my local machine so that I could change its permissions using "chmod".

The Bandit environment did not allow me to change the permissions as I expected because of permission restrictions.

It took me around 20 minutes to figure out the issue.

Eventually, I understood that I could save the private key locally, change its permissions, and use it to authenticate with SSH.

This level taught me the importance of understanding SSH authentication and file permissions.

---

Level 17–18

Task

There are two files in the home directory: "passwords.old" and "passwords.new".

The password for the next level is stored in "passwords.new" and is the only line that has changed between "passwords.old" and "passwords.new".

Steps Performed

1. Listed all files:
   
   ls -la

2. Initially displayed the contents of the new password file:
   
   cat passwords.new

3. Compared both files to identify the changed line:
   
   diff passwords.old passwords.new

4. Identified the changed line, which contained the password for the next level.

Problem Faced

Honestly, I did not face any major difficulties in this level.

The main thing I learned was the "diff" command, which I had not used before.

- "diff" – Compares two files line by line and displays the differences.
- "passwords.old" – The older version of the file.
- "passwords.new" – The updated version of the file.

Using "diff" made it much easier to identify the single changed line instead of manually comparing both files.

---

Overall Learning

During Day 04, I learned about SSH private key authentication, secure file transfers, networking utilities, SSL/TLS connections, port scanning, and file comparison.

I gained practical experience with commands such as "scp", "chmod", "ssh", "nc", "openssl", "nmap", "nano", and "diff".

The most challenging level was Level 16–17 because of the SSH private key and permission-related issues. However, solving it helped me understand how authentication works and how to troubleshoot Linux permission problems.

This day also improved my understanding of networking and secure communication.
