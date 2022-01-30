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

- Syntaxes for running 50 tasks in parallel (-t50, default 16)
```bash
# Dictionary-attack on target port 22 SSH.
hydra -t50 -l <UserName> -P <wordList.txt path> -vV <target IP> ssh

# Dictionalry-attack on a specific pathName
hydra -t50 -l <UserName> -P /usr/share/wordlists/rockyou.txt <target IP> http-get "/pathName"    
```
<br/>

### [**John the Ripper**](https://github.com/openwall/john)
- to guess the system's users' passwords from the hash values (or any common password in any hash value).
- The "_/etc/shadow_" shows the hash value of the "x" in "_/etc/passwd_". You can crack the hash value by
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
gobuster dir -u https://TargetIP.com -w /usr/share/dirbuster/directory-list-2.3-medium.txt -x php,phtml,css,js,json,html,txt,py,sh -t30
```
- brute-force using SecLists subdomains to discover virtual hosts, then use dirbuster to find the _flag_ in there
```bash
gobuster vhost -u http://TargetWebsite.com -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -t30

for vhost in subDomain1 subDomain2 subDomain3; do gobuster dir -u http://${vhost}.TargetWebsite.com -w /usr/share/dirbuster/directory-list-2.3-small.txt -x php,txt -t30 -o Output.txt ; done
```
<br/>

### [**WPScan**](https://github.com/wpscanteam/wpscan)
- black box WordPress vulnerability scanner. NOTE: You need to provide WPSan with an API Token so that it can look up vulnerabilities infos with https://wpvulndb.com. The free plan after registration allow 25 API requests a day.
- To install: _sudo apt update && sudo apt install wpscan_ for Debian/Ubuntu or _yay -S wpscan_ for ArchLinux, manually update by _wpscan --update_.
- Syntaxes to enumerte themes/plugins/userNames and brute-force passwords (flags: -t --max-threads, -o --output, -e --enumerate vpVulnerablePlugins apAllPlugins pPopularPlugins tPopularThemes uUserIDs, -P --passwords, -U --usernames, -v --verbose, --plugins-detection mixed/passsive/aggressive)
```bash
wpscan --url http(s)://<Target URL or IP address>
wpscan --url http(s)://<Target URL or IP address> --api-token <Generated_Token_from_your_login_profile>

wpscan --url <Target> --enumerate | tee Enumerate.txt
wpscan --url <Target> --usernames <FoundUserNames> --passwords <YourWordList.txt> | tee Credentials.txt
```
<br/>

### [**Nikto**](https://github.com/sullo/nikto)
- Scan web server for known vulnerabilities
```bash
nikto - h <target_IP> -p 80 -o nikto_results -F txt

nikto -id username:password -h <target_IP>:1234/path/
```
<br/>
