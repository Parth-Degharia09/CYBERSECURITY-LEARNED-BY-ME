Day 02 – OverTheWire Bandit (Level 5–10)

Level 5–6

Task

The password for the next level is stored in a file somewhere under the "inhere" directory and has all of the following properties:

- Human-readable
- 1033 bytes in size
- Not executable

Steps Performed

1. Listed the files and directories:
   
   ls

2. Entered the "inhere" directory:
   
   cd inhere

3. Used the "find" command to locate the required file:
   
   find . -type f -size 1033c ! -executable

4. Checked the file type:
   
   file filename

5. Displayed the file contents to retrieve the password:
   
   cat filename

Problem Faced

The "find" command initially gave me some difficulty because of its wide variety of uses. I first tried using "grep", but it returned multiple files with similar values. After figuring it out, I used the "find" command successfully.

- "." – Represents the current directory.
- "-type f" – Searches only for regular files.
- "-size 1033c" – Searches for files that are exactly 1033 bytes ("c" represents bytes).
- "! -executable" – Excludes executable files ("!" means NOT).

Combining these conditions helped me locate the required file.

---

Level 6–7

Task

The password for the next level is stored somewhere on the server and has the following properties:

- Owned by user "bandit7".
- Owned by group "bandit6".
- 33 bytes in size.

Steps Performed

1. Listed all files, including hidden files:
   
   ls -la

2. Searched for the file using its ownership and size:
   
   find . -user bandit7 -group bandit6 -size 33c

3. Used the following command to hide permission errors:
   
   find . -user bandit7 -group bandit6 -size 33c 2>/dev/null

4. Displayed the contents of the identified file:
   
   cat filename

Problem Faced

The first "find" command displayed many permission-denied errors. However, it also contained the required answer, which took some time to locate.

After researching, I learned how to redirect error messages using "2>/dev/null".

- "2" – Represents standard error (stderr).
- ">" – Redirects the output.
- "/dev/null" – Discards the redirected output.

This helped hide permission errors and made the result easier to read.

---

Level 7–8

Task

The password for the next level is stored in the file "data.txt", next to the word "millionth".

Steps Performed

1. Listed the files:
   
   ls -la

2. Used "grep" to search for the word "millionth":
   
   grep millionth data.txt

Problem Faced

As a beginner, I initially used the "cat" command to display the entire file. It dumped a huge amount of text into my terminal, making it difficult to find the required information.

I had to reset my terminal. After that, I used the "grep" command, which helped me search directly for the word "millionth" instead of displaying the entire file.

---

Level 8–9

Task

The password for the next level is stored in the file "data.txt" and is the only line of text that occurs only once.

Steps Performed

1. Listed the files:
   
   ls -la

2. Sorted the lines and filtered out the unique line:
   
   sort data.txt | uniq -u

Problem Faced

Initially, I used "uniq -u data.txt", but it did not give me the expected result because the "uniq" command only detects adjacent duplicate lines.

After that, I learned to use the "sort" command before "uniq".

- "sort" – Sorts the lines of a file.
- "|" – Pipeline operator, which passes the output of one command to another.
- "uniq -u" – Displays only lines that occur exactly once.

Combining both commands helped me find the required password.

---

Level 9–10

Task

The password for the next level is stored in the file "data.txt" in one of the few human-readable strings, preceded by several "=" characters.

Steps Performed

1. Listed the files:
   
   ls -la

2. Used the "strings" command to extract human-readable strings:
   
   strings data.txt

3. Used "grep" to filter strings containing the "=" character:
   
   strings data.txt | grep '='

Problem Faced

Initially, I used the "strings" command, which printed many human-readable strings from the file. Although I could still find the password in the output, it was difficult to identify the required information.

After that, I combined "strings" with "grep" to filter the output and make the search easier.

- "strings" – Extracts printable human-readable strings from a file.
- "grep '='" – Searches for lines containing the "=" character.
- "|" – Passes the output of "strings" to "grep".

This made finding the password much easier.

---

Overall Learning

During Day 02, I learned how to search for files based on specific conditions, filter error messages, search for particular words, identify unique lines, and extract human-readable strings.

I also gained practical experience with commands such as "find", "grep", "sort", "uniq", and "strings", along with understanding how to combine commands using pipes and redirection
