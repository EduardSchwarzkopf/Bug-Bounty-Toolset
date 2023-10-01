# API Bug Bounty

## Reconnaissance

### Passive

#### Google Dorking

Website: https://www.google.com/

Straight up search on Google like

`<target_name> api`

More specific searches:
- `intitle:"api" site:<company_domain>`
- `inurl:"/api/v1" site:"<company_domain>"`
- `intitle:json site:<company_domain>`

#### Github

Website: https://github.com/

Again, do a direct search for the api:

`<target_name> api`

- Search in issues
    - Also search for keys
    - `<target_name> api key`
    - `api key exposed <target_name>`

`extension:json <target_name>`

You can also make a search for api keys if you know the naming convention, e.g.

`shodan_api_key`

Search for common headers:

`"authorization: Bearer" <target_name>`

Search for swagger files:
`filename:swagger.json <target_name>`

#### Shodan

Website: https://www.shodan.io/

As always, just use a direct search first:

`<target_name>`

Look for ports as well:

`<target_name> port:443`

Search for the Application Header:

`"content-type: application/json" <target_name>`

#### Wayback Machine

Website: https://archive.org/web/

Use the Wayback machine to search for the API docs of your target and check for old endpoints, that were implemented, but were simply removed from the docs, but still work