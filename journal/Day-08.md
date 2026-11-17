Day 08 – Levels 28–34

Level 28–29

Task

Clone the Git repository from the local machine and find the password for the next level. The repository is available through SSH on port "2220".

Steps Performed

1. Clone the repository:
   git clone ssh://bandit28-git@bandit.labs.overthewire.org:2220/home/bandit28-git/repo
2. Enter the Bandit 28 password when prompted.
3. Navigate into the repository:
   cd repo
4. List all files:
   ls -la
5. Read the README file:
   cat README.md
6. View the commit history:
   git log --oneline
7. Inspect the relevant commit to find the previous version of the README:
   git show <commit-hash>
8. Return to the parent directory and remove the cloned repository:
   cd ..
rm -rf repo

Problem Faced

I did not know about the "git log" and "git show" commands. After learning how to use them, the level became fairly easy. I realised that learning basic Git commands before attempting these levels would have helped.

Level 29–30

Task

Clone the Git repository from the local machine and find the password for the next level.

Steps Performed

1. Clone the repository:
   git clone ssh://bandit29-git@bandit.labs.overthewire.org:2220/home/bandit29-git/repo
2. Enter the Bandit 29 password when prompted.
3. Navigate into the repository:
   cd repo
4. List all files:
   ls -la
5. Read the README file:
   cat README.md
6. List all branches, including remote branches:
   git branch -a
7. Switch to the development branch:
   git checkout dev
8. Read the README file again:
   cat README.md
9. Return to the parent directory and remove the cloned repository:
   cd ..
rm -rf repo

Problem Faced

I did not face any problems during this level. It was straightforward once I understood how to list and switch between Git branches.

Level 30–31

Task

Clone the Git repository from the local machine and find the password for the next level.

Steps Performed

1. Clone the repository:
   git clone ssh://bandit30-git@bandit.labs.overthewire.org:2220/home/bandit30-git/repo
2. Enter the Bandit 30 password when prompted.
3. Navigate into the repository:
   cd repo
4. List all files:
   ls -la
5. Read the README file:
   cat README.md
6. List the Git tags:
   git tag
7. Inspect the secret tag:
   git show secret

Problem Faced

I already knew about Git tags, so I did not face much difficulty. I just needed to learn how to inspect a particular tag using "git show".

Level 31–32

Task

Clone the Git repository from the local machine and find the password for the next level by adding the required file and pushing it to the remote repository.

Steps Performed

1. Clone the repository:
   git clone ssh://bandit31-git@bandit.labs.overthewire.org:2220/home/bandit31-git/repo
2. Enter the Bandit 31 password when prompted.
3. Navigate into the repository:
   cd repo
4. List all files:
   ls -la
5. Create "key.txt" and add the required text:
   echo "May I come in?" >> key.txt
6. Check the file contents:
   cat key.txt
7. Check the Git ignore rules:
   cat .gitignore
8. Force Git to add the ignored file:
   git add -f key.txt
9. Commit the changes:
   git commit -m "Add key.txt"
10. Push the changes to the remote repository:
    git push

Problem Faced

I forgot about ".gitignore", which prevents specified files from being tracked by Git. After remembering this, I used "git add -f" to force Git to add "key.txt" even though it was ignored.

Level 32–33

Task

Escape from the restricted shell where commands are automatically converted to uppercase.

Steps Performed

1. Connect to Bandit 32:
   ssh bandit32@bandit.labs.overthewire.org -p 2220
2. Enter the Bandit 32 password.
3. List the files:
   ls -la
4. Enter the following:
   $0
5. List the files again:
   ls -la
6. Check the current user:
   whoami
7. Read the password for Bandit 33:
   cat /etc/bandit_pass/bandit33
8. Exit the shell:
   Ctrl + D
9. Press "Ctrl + D" again if needed to close the remaining session.

Problem Faced

Every command I entered was automatically converted to uppercase in this level. I learned that "$0" can be used to start another shell, allowing me to escape the restricted shell and execute normal commands.

Level 33–34

Task

There is currently no Level 34. This is the final available level of the Bandit game.

Steps Performed

1. List all files:
   ls -la
2. Read the README file:
   cat README.txt
3. The README displayed a congratulatory message confirming that all available Bandit levels had been completed.

Problem Faced

There was no difficulty in this level. It simply confirmed that I had completed all the currently available levels of the Bandit wargame.

Overall Learning

- Learned how to inspect Git commit history using "git log".
- Understood how to inspect previous commits and their contents using "git show".
- Learned how to list and switch between Git branches using "git branch -a" and "git checkout".
- Understood how Git tags work and how to inspect them using "git show".
- Learned how ".gitignore" works and how to force-add an ignored file using "git add -f".
- Practised committing and pushing changes to a remote Git repository.
- Learned how "$0" can help escape a restricted shell.
- Completed all currently available levels of the OverTheWire Bandit wargame.
