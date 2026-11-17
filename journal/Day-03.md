Day 03 – OverTheWire Bandit (Level 10–13)

Level 10–11

Task

The password for the next level is stored in the file "data.txt", which contains Base64 encoded data.

Steps Performed

1. Listed the files:
   
   ls -la

2. Decoded the Base64 encoded data:
   
   base64 -d data.txt

Problem Faced

Initially, I did not know about Base64 encoding. After researching it, I learned that Base64 is a binary-to-text encoding scheme that uses 64 printable characters to represent data.

I read the manual page using "man base64" and understood how the decoding process works.

The "-d" option is used to decode the Base64 encoded data and retrieve the original text.

---

Level 11–12

Task

The password for the next level is stored in the file "data.txt", where all lowercase (a–z) and uppercase (A–Z) letters have been rotated by 13 positions.

Steps Performed

1. Listed the files:
   
   ls -la

2. Displayed the contents of the file:
   
   cat data.txt

3. Used the "tr" command to decode the ROT13 encoded text:
   
   cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

Problem Faced

Initially, I did not understand how ROT13 worked. After researching, I learned that ROT13 is a letter substitution technique in which every letter is replaced by the letter 13 positions ahead in the alphabet.

I also learned about the "tr" command, which is used to translate or delete characters.

- "tr" – Translates or deletes characters.
- "'A-Za-z'" – Represents all uppercase and lowercase English letters.
- "'N-ZA-Mn-za-m'" – Maps each letter to the character 13 positions ahead.
- "|" – Passes the output of one command to another.

After understanding the character mapping, I successfully decoded the password.

---

Level 12–13

Task

The password for the next level is stored in the file "data.txt", which is a hexdump of a file that has been repeatedly compressed.

For this level, it is useful to create a temporary directory using "mktemp -d", copy the data file into it, and rename files using "mv" while repeatedly decompressing them.

Steps Performed

1. Listed the files:
   
   ls -la

2. Created a temporary directory:
   
   mktemp -d

3. Entered the temporary directory created by the previous command:
   
   cd /tmp/directory-name

4. Copied the original data file into the temporary directory:
   
   cp ~/data.txt .

5. Checked the copied file:
   
   ls -la

6. Read the manual page for "xxd":
   
   man xxd

7. Reversed the hexdump to retrieve the original binary file:
   
   xxd -r data.txt data.bin

8. Identified the file type:
   
   file data.bin

9. Depending on the file type, renamed and decompressed the file.
   
   If the file is GZIP:
   
   mv data.bin data.gz
gunzip data.gz
   
   If the file is BZIP2:
   
   mv data.bin data.bz2
bunzip2 data.bz2
   
   If the file is TAR:
   
   mv data.bin data.tar
tar -xf data.tar

10. After each decompression, checked the extracted files and their types:
    
    ls -la
file filename

11. Repeated the decompression process according to the file type until the file command identified the final file as ASCII text.

12. Displayed the final file contents:
    
    cat final-file

Problem Faced

This level was more challenging because I had to research different compression formats, including TAR, BZIP2, and GZIP, along with understanding how to reverse a hexdump.

The main difficulty I faced was after extracting TAR files. The extraction produced files with names such as "data5.bin", and initially, I did not know what to do with those files.

After researching, I understood that the process had to be repeated on the newly extracted files.

I learned to:

- Use "file" to identify the type of a file.
- Use "ls -la" to check the extracted files.
- Rename files using "mv" according to their compression format.
- Use the appropriate decompression command.
- Repeat the process until the final file contains readable ASCII text.

This level helped me understand how different compression formats work and how to handle nested compressed files.

---

Overall Learning

During Day 03, I learned about Base64 decoding, ROT13 encryption, character translation, hexdumps, and different compression formats.

I gained practical experience with commands such as "base64", "tr", "xxd", "file", "gzip", "bzip2", "tar", "mv", and "mktemp".

The most challenging part was Level 12–13, where I had to repeatedly identify and decompress files using different tools. It improved my ability to research commands, read manual pages, and solve Linux-based challenges independently.
