# Useful pentest tools
I am gathering and uploading useful pentest tools here.

### [**SecLists**](https://github.com/danielmiessler/SecLists)
- a collection of multiple types of lists used during security assessments (usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells). In Kali you can install by:
```bash
sudo apt -y install seclists
```
<br/>

### [**Hydra**](https://github.com/vanhauser-thc/thc-hydra)
- brute-force attack (mainly dictionary attack) tool.
- Install:
```bash
git clone https://github.com/vanhauser-thc/thc-hydra ~/Downloads/thc-hydra && cd ~/Downloads/thc-hydra
./configure
make
make install
```
<br/>

- Hydra syntax to dictionary-attack on target port 22 SSH.
```bash
hydra -t 16 -l USERNAME -P <wordList.txt path> -vV <target IP> ssh
```
<br/>

### [**John the Ripper**](https://github.com/openwall/john)
- to guess the system's users' passwords from the hash values (or any common password in any hash value).
- The "_/etc/shadow_" shows the hash value of the "x" in "_/etc/passwd_". You can crack the hash value by:
```bash
sudo unshadow /etc/passwd /etc/shadow > unshadowed.txt && john unshadowed.txt && john --show unshadowed.txt
```
- Or you can use YourWordList.txt
```bash
john --wordlist=/usr/share/wordlists/YourWordList.txt --format=sha512crypt unshadowed.txt
```
<br/>

### [fuzzdb SQLi platform detection list](https://github.com/fuzzdb-project/fuzzdb/blob/master/attack/sql-injection/detect/xplatform.txt):
- (for Burp Suite payload in intruder): brute force attack to get the server response status 200.
