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


---
## ffuf

https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html

### Recursion
`ffuf -u https://target.io/FUZZ -w ./wordlist -recursion`

### File extensions
`ffuf -u https://target.io/FUZZ -w ./wordlist -recursion -e .bak`

## Silent Mode
`ffuf -u https://target.io/FUZZ -w ./wordlist.txt -s | tee ./output.txt`

This will output just the results and place them into a file, alternativly pipe the output directly into a program.

## Slow down
`-p` flag to slow down requests, check `-h` for more information
