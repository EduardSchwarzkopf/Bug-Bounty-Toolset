# Bug-Bounty-Toolset

-----------
## General Approach

- Write down stuff, that might be interesting
- Think like a black hat hacker -> grab all dataa you can get
- 

## Passive recon

### Useful google dorks

- `intitle:"api" site:example.com`
- `inurl:"api/v1" site:example.com`
- `intitle:json site:example.com`

### useful github dorks

- search for api keys e.g. `api keys exposed` -> issue search
- `exension:json {username}` -> repository search
- search for naming of api keys, e.g.: `shodan_api_key` -> repos, issues, discussion
- search for common headers `"authorization: Bearer"`
- search for swagger file `filename:swagger.json`

### shodan dorks

- generic search
- search for ports `port:{port}`
- `example.com "content-type: application/json"`
- `wp-json` for wordpress APIs

### wayback machine

- use wayback machine to check for API docs
- here you might find old endpoints that are still available and are just remove from the docs


## Active recon

### scan target

#### nmap

![image](https://user-images.githubusercontent.com/48969167/229360585-e6770764-cda6-4530-8bba-13bb4e4bcb68.png)


1. scan defaults: `nmap -sC -sV {target_ip}`
2. decoy scan: `sudo nmap -sS -p {port} -D RND:{number of decoys} -e {interface} {target_ip}` 
<br>e.g. `sudo nmap -sS -p80 -D RND:20 -e eth0 scanme.nmap.org`  
4. scan specific ports `nmap -sV {target_ip} -p {port}`
5. ping scan: `nmap -sn 192.168.1.0/24`
6. top 20 ports (replace 20 with any number): `nmap --top-ports 20 {target_ip}`
7. Getting the OS: `nmap -O {target_ip}`
8. Getting everyhting from target (OS, Version, Trace): `nmap -A {target_ip}`

**Usage of nmap scripts (It is noisy)**:
Location: `/usr/share/nmap/scripts`

Usage:

- Run all test tagged as `default`: `nmap --script default {target_ip}`
- Run a single script: `nmap --script 'http-auth' {target_ip}`
- Run all http scripts: `nmap --script 'http-*' {target_ip}`

Common scripts:

- `banner`: Get service banners from the services
- `ssl-enum-ciphers` use with the `-p 443`: Get the TLS version (It is noisy, slow it down if you want to be under the radar)
- `http-methods`: Get allowed HTTP Methods
- `http-enum`: Find folders on the target

**nmap flag	Description**
- `sV`	Attempts to determine the version of the services running
- `p` <x> or -p-	Port scan for port <x> or scan all ports
- `Pn`	Disable host discovery and just scan for open ports
- `A`	Enables OS and version detection, executes in-build scripts for further enumeration 
- `sC`	Scan with the default nmap scripts
- `v`	Verbose mode
- `sU`	UDP port scan
- `sS`	TCP SYN port scan
  
  
#### gobuster

GoBuster is a tool used to brute-force URIs (directories and files), DNS subdomains and virtual host names. For this machine, we will focus on using it to brute-force directories.

Usage: `gobuster dir -u http://<ip/domain>:<port> -w <word list location>`
  
**Flags**
- `-e`	Print the full URLs in your console
- `-u`	The target URL
- `-w`	Path to your wordlist
- `-U` and -P	Username and Password for Basic Auth
- `-p` <x>	Proxy to use for requests
- `-c` <http cookies>	Specify a cookie for simulating your auth
  

#### nikto
Scan with nikto to check for missconfigurations: `nikto -h http://example.com`
Check for missing headers, when it comes to APIs


#### OWASP Zap

1. Manual Explorer
2. Add URL
3. Click Launch Browser
4. Click on the shield icon next to the url and turn off "Enhanced Tracking Protection"
5. Click on Continue to your target
6. On the right site, start the attack mode
7. Use the app all features of the app
8. On the right site, start an active scan (ressource heavy)
9. Go back to Zap
10. On right site, right-click on the target folder -> Add new Context -> Ok
11. Click on the small target icon in the top left corner, to have a better overview

To skip certain scans, click on the small health monitor icon in the middle next to the progress bar and disable scans you don't want. E.g. SOAP Action Spoofing, SOAP XML Injection, Script Active Scan Rules

Review the results under **Alerts** tab. Select the alert and check the request and response, if it is a valid alert.

#### amass -> get potential api entries

1. get sources with: `amass enum -list`
2. search with: `amass enum -d <target_domain/ip> | grep api`

#### gobuster -> directory brute force (non-api related)

(maybe get an api wordlist for this)
1. root check: `gobuster dir -u <target>:<port> -w /usr/share/wordlists/dirbuster/<wordlist> --wildcard -b 200`
2. specific check `gobuster dir -u <target_domain>:<port>/<path> -w /usr/share/wordlists/dirbuster/<wordlist>`
3. use `-b <status_code>` to filter out unwanted results e.g. 401, 200, etc.
4. use `--wildcard` to scan all

### Browser dev tools (F12 key)

1. Network Manager to see where requests are going. Maybe filter by XHR
2. Add the URL column, if not there
3. search for `api`

**Tip**: Import a request via cURL. Right click on a request in the network tab. Switch to Postman, click import -> Raw text and paste the cURL request in

## Test Flow

- Opting in
- Opting out
- use the companies domain as sign-up 
  - maybe change it later, if confirmation is required
- Use sandbox PayPal / Credit Cards
  - On bigger company, try another country
- Invite Socket Account and try the link with another Socket account
- Always alter requests
- check tokens
