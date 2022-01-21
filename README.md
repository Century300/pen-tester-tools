# Useful pentest tools
I am gathering and uploading useful pentest tools here.

### **Wordlists**
- [**SecLists**](https://github.com/danielmiessler/SecLists): a collection of multiple types of lists used during security assessments (usernames, passwords, URLs, sensitive data patterns, fuzzing payloads, web shells). In Kali you can install by:
```bash
sudo apt -y install seclists
```
- dirbuster wordlists from [OWASP DirBuster](https://www.kali.org/tools/dirbuster/). Follow [this instruction](https://saulenas.com/How-to-install-DirBuster-on-Linux/) to install in any Linux distros. Install in arch by using AUR (Arch User Repository):
```
yay -S dirbuster
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

### [**fuzzdb** SQLi platform detection list](https://github.com/fuzzdb-project/fuzzdb/blob/master/attack/sql-injection/detect/xplatform.txt)
- (for Burp Suite payload in intruder): brute force attack to get the server response status 200.
<br/>

### [**Gobuster**](https://github.com/OJ/gobuster)
- to brute-force URIs & DNS subdomains beside the [OWASP DirBuster](https://www.kali.org/tools/dirbuster/) tool
- adding target IP or URL to /etc/hosts if necessary to run gobuster
```bash
echo "10.10.200.xxx Target.com subdomain.Target.com" >> /etc/hosts

```
- brute-force using dirbuster wordlist using 30 concurrent threads (optional flag: -v verbose, -x fileExtensions)
```bash
gobuster dir -u https://TargetIP.com -w /usr/share/dirbuster/directory-list-2.3-medium.txt -t30 -o 
```
- brute-force using SecLists subdomains to discover virtual hosts, then use dirbuster to find the _flag_ in there
```bash
gobuster vhost -u http://TargetWebsite.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -t30

for vhost in subDomain1 subDomain2 subDomain3; do gobuster dir -u http://${vhost}.TargetWebsite.com -w /usr/share/dirbuster/directory-list-2.3-small.txt -x php,txt -t30 -o Output.txt ; done
```
<br/>