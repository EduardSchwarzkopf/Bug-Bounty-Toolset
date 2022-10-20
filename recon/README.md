Use with TomNomNom Tools (https://github.com/tomnomnom)

Create a wildcard file `wildcard` with all wildcard domains
```
example.com
example.de
```

Find subdomains with:
`cat wildcards | assetfinder --subs-only | anew domains`

`wildcards` is the file with our wildcards, `assetfinder` is a tool to quickly search for subdomains and `anew` puts all unique findings in a `domains` file for us  


-----
Search engines to lookup history data of IPs, behind CDN:
- https://search.censys.io
- shodaon.i
