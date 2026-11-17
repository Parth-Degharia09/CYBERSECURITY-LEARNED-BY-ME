Day 05 – OverTheWire Bandit (Level 18–23)

Level 18–19

Task

The password for the next level is stored in a file named "readme" in the home directory. Unfortunately, someone has modified ".bashrc" to log you out whenever you connect through SSH.

Steps Performed

1. Connected to Bandit 18 using SSH and directly executed the "cat" command instead of opening an interactive shell:
   
   ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

2. Retrieved the password directly from the output.

Problem Faced

Honestly, I did not face any major problems in this level. The main thing I learned was that SSH allows us to execute commands directly on a remote machine without opening an interactive shell.

This helped me bypass the automatic logout caused by the modified ".bashrc" file.

---

Level 19–20

Task

To gain access to the next level, we need to use the SETUID binary in the home directory.

We must execute the binary without arguments to understand how it works. The password for the next level can then be retrieved from "/etc/bandit_pass" using this binary.

Steps Performed

1. Listed all files:
   
   ls -la

2. Executed the SETUID binary:
   
   ./bandit20-do

3. Followed the instructions displayed by the binary and used it to read the next level's password:
   
   ./bandit20-do cat /etc/bandit_pass/bandit20

4. Retrieved the password for Bandit 20.

Problem Faced

Initially, I thought I had to use a separate "setuid" command to access the next level.

However, after executing the binary without arguments, I understood that it already handled the elevated permissions.

I learned that SETUID allows an executable to run with the permissions of its file owner rather than the permissions of the user executing it.

This binary allowed me to execute commands with Bandit 20's privileges and retrieve the password.

---

Level 20–21

Task

There is a SETUID binary in the home directory that connects to localhost on a port specified as a command-line argument.

It reads a line of text from that connection and compares it with the password of Bandit 20. If the password is correct, it sends the password for Bandit 21 back through the connection.

Steps Performed

1. Listed the files:
   
   ls -la

2. Executed the binary to understand its usage:
   
   ./suconnect

3. Started a Netcat listener on a port:
   
   nc -lvp 12345

4. Since the port was already in use, I selected another port:
   
   nc -lvp 64325

5. On the listener terminal, entered the current Bandit 20 password.

6. Opened another terminal and logged in to Bandit 20.

7. Executed the SETUID binary with the listener's port:
   
   ./suconnect 64325

8. Received the password for Bandit 21 through the Netcat connection.

Problem Faced

Initially, I only knew a few Netcat options, such as "-p", "-l", and "-v".

After reading the manual page for "nc", I understood their purpose:

- "nc" – Netcat networking utility.
- "-l" – Puts Netcat into listening mode.
- "-p" – Specifies the port number.
- "-v" – Enables verbose output, providing more information about the connection.

The first port I selected was already in use, so I switched to another port, "64325".

After understanding how the listener and SETUID binary communicate, I successfully retrieved the password.

---

Level 21–22

Task

A program is running automatically at regular intervals using Cron, a time-based job scheduler.

We need to inspect the configuration files inside "/etc/cron.d/" to identify the scheduled job and understand which command is being executed.

Steps Performed

1. Listed the files:
   
   ls -la

2. Checked the Cron configuration directory:
   
   ls /etc/cron.d

3. Read the configuration file for Bandit 22:
   
   cat /etc/cron.d/cronjob_bandit22

4. Identified the script being executed by the Cron job.

5. Read the script:
   
   cat /usr/bin/cronjob_bandit22.sh

6. Checked the temporary file created by the script:
   
   cat /tmp/filename

7. Retrieved the password for the next level.

Problem Faced

I did not face any major technical difficulties in this level. However, I was unfamiliar with Cron and how it works.

After researching, I learned that Cron is a time-based job scheduler in Linux that automatically executes commands or scripts at specified intervals.

I also learned that:

- "/etc/cron.d/" – Contains configuration files for scheduled Cron jobs.
- "cat" – Helps inspect the configuration and script contents.
- "/usr/bin/" – Commonly contains executable programs and scripts.

This level helped me understand how automated tasks work in Linux.

---

Level 22–23

Task

A program is running automatically at regular intervals using Cron.

We need to inspect the configuration inside "/etc/cron.d/", identify the script being executed, and understand how it retrieves and stores the password.

Steps Performed

1. Listed the files:
   
   ls -la

2. Checked the Cron configuration directory:
   
   ls /etc/cron.d/

3. Inspected the Cron job configuration:
   
   cat /etc/cron.d/cronjob_bandit23

4. Read the script being executed:
   
   cat /usr/bin/cronjob_bandit23.sh

5. Initially tried accessing the password using the variable:
   
   cat /etc/bandit_pass/$myname
   
   However, this did not work because the variable was not defined in my current shell.

6. After understanding the script, I used the following command to generate the required filename:
   
   echo I am user bandit23 | md5sum | cut -d ' ' -f 1

7. The command generated the following hash:
   
   8ca319486bfbbc3663ea0fbe81326349

8. Used the generated hash to access the temporary file:
   
   cat /tmp/8ca319486bfbbc3663ea0fbe81326349

9. Retrieved the password for Bandit 23.

Problem Faced

This was the first level where I relied heavily on AI to understand the method after Step 8 because I could not figure out the solution independently at that time.

However, AI explained how the script worked and why the commands were necessary.

I learned that:

- "echo" – Prints the specified text.
- "md5sum" – Generates an MD5 hash of the input.
- "|" – Passes the output of one command to another.
- "cut" – Extracts specific sections from text.
- "-d ' '" – Uses a space as the delimiter.
- "-f 1" – Selects the first field.

The Cron script uses the username to generate a predictable MD5-based filename. Since the script runs as Bandit 23, the required input is:

echo I am user bandit23

The resulting hash identifies the temporary file where the script stores the password.

This level helped me understand how shell variables, command pipelines, MD5 hashing, and automated scripts work together.

---

Overall Learning

During Day 05, I learned about SSH command execution, SETUID binaries, Netcat listeners, Cron jobs, shell variables, MD5 hashing, and command pipelines.

I gained practical experience with commands such as "ssh", "cat", "nc", "ls", "md5sum", "cut", and "echo".

The most interesting levels were Level 20–21 and Level 22–23 because they required understanding communication between processes and how automated scripts work.

I also realized that researching unfamiliar commands and reading scripts written by others are important skills when working with Linux and cybersecurity challenges.
