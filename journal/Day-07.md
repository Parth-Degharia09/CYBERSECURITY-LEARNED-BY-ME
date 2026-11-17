Day 07 – OverTheWire Bandit (Level 25–28)

Level 25–26

Task

Logging in to Bandit 26 from Bandit 25 should be fairly easy. However, the shell for user "bandit26" is not "/bin/bash", but something else.

The objective is to identify the shell, understand how it works, and find a way to escape from it.

Steps Performed

1. Listed all files:
   
   ls -la

2. Checked the shell assigned to Bandit 26:
   
   cat /etc/passwd | grep bandit26

3. Inspected the script responsible for launching the restricted environment:
   
   cat /usr/bin/showtext

4. Reduced the terminal height:
   
   stty rows 5

5. Logged in to Bandit 26 using the private SSH key:
   
   ssh -i bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org

6. When the "--More--" prompt appeared, pressed:
   
   v
   
   This opened the Vim editor.

7. Pressed "Esc" to enter Vim command mode.

8. Changed the shell used by Vim:
   
   :set shell=/bin/bash

9. Started a Bash shell from Vim:
   
   :shell

10. Retrieved the password for Bandit 26:
    
    cat /etc/bandit_pass/bandit26

Understanding the Commands

- "cat /etc/passwd" – Displays information about system user accounts, including their assigned login shells.
- "grep bandit26" – Filters the output to show the entry for Bandit 26.
- "cat /usr/bin/showtext" – Displays the script used to launch the restricted environment.
- "stty rows 5" – Changes the terminal's reported height to five rows. This makes the "more" pager pause and provides an opportunity to open Vim.
- "v" – Opens Vim from the "more" pager.
- ":set shell=/bin/bash" – Changes the shell Vim uses when executing shell commands.
- ":shell" – Starts the configured shell from inside Vim.

Problem Faced

I initially had no idea what "stty rows 5" did. After researching, I understood that it changes the terminal's reported number of rows.

This was important because the restricted shell used the "more" pager, and reducing the terminal height helped me access its interactive features.

Honestly, this was one of the most difficult levels for me, especially because I was using WSL. I needed AI assistance to understand the process and get through the challenge.

This level taught me how terminal settings, pagers, Vim, and restricted shells can interact with each other.

---

Level 26–27

Task

After successfully escaping the restricted shell in the previous level, the objective is to retrieve the password for Bandit 27.

Steps Performed

1. Connected to Bandit 26 using the private SSH key:
   
   ssh -i bandit26.sshkey -p 2220 bandit26@bandit.labs.overthewire.org

2. When the "--More--" prompt appeared, pressed "v" to open Vim.

3. Pressed "Esc" to enter command mode.

4. Configured Vim to use Bash:
   
   :set shell=/bin/bash

5. Escaped into the Bash shell:
   
   :shell

6. Used the provided SETUID binary to retrieve the password:
   
   ./bandit27-do cat /etc/bandit_pass/bandit27

7. Retrieved the password for Bandit 27.

Problem Faced

I did not face any major difficulties in this level. However, I experienced a few minor issues because of WSL and the restricted shell environment.

My recommendation is to practise these challenges using WSL before completely shifting to a full Linux environment. It helps build familiarity with Linux commands and terminal operations.

This level also helped reinforce what I learned in the previous challenge about Vim and restricted shells.

---

Level 27–28

Task

There is a Git repository available at:

ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo

The password for the user "bandit27-git" is the same as the password for "bandit27".

The objective is to clone the repository from the local machine, not from the OverTheWire server, and find the password for the next level.

Steps Performed

1. Created a temporary directory on my local machine:
   
   mkdir /tmp/parth27

2. Entered the directory:
   
   cd /tmp/parth27

3. Cloned the Git repository using SSH:
   
   GIT_SSH_COMMAND="ssh -p 2220" git clone ssh://bandit27-git@bandit.labs.overthewire.org/home/bandit27-git/repo

4. Entered the cloned repository:
   
   cd repo

5. Listed the repository contents:
   
   ls -la

6. Read the README file:
   
   cat README

7. Retrieved the password for Bandit 28.

Problem Faced

Honestly, I did not face any major difficulties in this level. The instructions were fairly clear, and everything needed to complete the challenge was provided.

The main thing I learned was how to clone a remote Git repository using SSH and a custom port.

I also understood that Git operations such as cloning can be performed directly from my local machine without needing to work inside the remote OverTheWire server.

---

Overall Learning

During Day 07, I learned about restricted Linux shells, terminal configuration, Vim shell escapes, SETUID binaries, and Git repository cloning over SSH.

I gained practical experience with commands and tools such as "stty", "more", "vim", "grep", "cat", "ssh", "git clone", and "ls".

The most challenging part was Level 25–26 because it required understanding how to escape a restricted shell using the "more" pager and Vim.

Level 27–28 was a good introduction to working with remote Git repositories through SSH.

Overall, these levels improved my confidence in Linux terminal operations and helped me understand how different Linux tools can be combined to solve practical challenges.
