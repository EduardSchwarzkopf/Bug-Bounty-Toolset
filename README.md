# Bug-Bounty-Toolset

-----------
## General Approach

- Write down stuff, that might be interesting
- Think like a black hat hacker -> grab all dataa you can get
- 

## Passive recon

### Useful google dorks

- `intitle:"api" site:<target_domain>`
- `inurl:"api/v1" site:<target_domain>`
- `intitle:json site:<target_domain>`

### useful github dorks

- search for api keys e.g. `api keys exposed` -> issue search
- `exension:json <target>` -> repository search
- search for naming of api keys, e.g.: `shodan_api_key` -> repos, issues, discussion
- search for common headers `"authorization: Bearer"`
- search for swagger file `filename:swagger.json`

### shodan dorks

- generic search
- search for ports `port:<port>`
- `<target> "content-type: application/json"`
- `wp-json` for wordpress APIs

### wayback machine

- use wayback machine to check for API docs
- here you might find old endpoints that are still available and are just remove from the docs

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
