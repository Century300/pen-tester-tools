# Useful pentest tools
I gathered useful pentest tools here.

## Instruction
- apt -y install seclists : (in Kali) [SecLists](https://github.com/danielmiessler/SecLists) is a collection of multiple types of lists used during security assessments (usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells)
-   git clone https://github.com/vanhauser-thc/thc-hydra _then_ ./configure _then_ make _then_ make install : Hydra brute-force attack (mainly dictionary attack) tool. _Syntax_ hydra -t 16 -l USERNAME -P <wordList.txt path> -vV <target IP> ssh _to dictonary-attack on target port 22 SSH_
