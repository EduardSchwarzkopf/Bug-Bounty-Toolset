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
1. scan defaults: `nmap -sC -sV {target_ip}`
2. scan all ports: `nmap -p- {target_ip}`
3. scan specific ports `nmap -sV {target_ip} -p {port}`
4. Check the service under the port via browser

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
