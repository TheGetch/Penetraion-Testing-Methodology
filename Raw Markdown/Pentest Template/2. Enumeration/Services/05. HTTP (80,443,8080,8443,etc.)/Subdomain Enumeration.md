Subdomain Enumeration

## Subdomain Enumeration

### Brute Force with ffuf:
```
$ ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -u http://sneakycorp.htb/ -H "Host: FUZZ.sneakycorp.htb" -fs 185
```

### sublist3r
```
sublist3r -d google.com
```

### subfinder

```
subfinder -d example.com
```

Add keys to:

`/home/<user>/.config/subfinder/config.yaml`