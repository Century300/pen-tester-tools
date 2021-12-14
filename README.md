# Useful pentest tools
I am gathering and uploading useful pentest tools here.

## Instruction
- apt -y install seclists : (in Kali) [**SecLists**](https://github.com/danielmiessler/SecLists) is a collection of multiple types of lists used during security assessments (usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells).
- git clone https://github.com/vanhauser-thc/thc-hydra _then_ ./configure _then_ make _then_ make install : **Hydra** brute-force attack (mainly dictionary attack) tool. _Syntax_ hydra -t 16 -l USERNAME -P <wordList.txt path> -vV <target IP> ssh _to dictonary-attack on target port 22 SSH_.
- sudo unshadow /etc/passwd /etc/shadow > unshadowed.txt && john unshadowed.txt && john --show unshadowed.txt (_or_ john --wordlist=/usr/share/wordlists/YourWordList.txt --format=sha512crypt unshadowed.txt) : use [**John the Ripper**](https://github.com/openwall/john) to guess the system's users' passwords from the hash values (or any common password in any hash value). the /etc/shadow shows the hash value of the "x" in /etc/passwd.
- [fuzzdb SQLi platform detection list](https://github.com/fuzzdb-project/fuzzdb/blob/master/attack/sql-injection/detect/xplatform.txt) (for Burp Suite payload in intruder): brute force attack to get the server response status 200.
