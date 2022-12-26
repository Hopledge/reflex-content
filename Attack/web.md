# Web

???+ tip "DNS Enumeration"
    | Commands                                                              | Description                   |
    |-----------------------------------------------------------------------|-------------------------------|
    | `gobuster dns -d target.net -w ~/wordlists/subdomains.txt --wildcard` | Subdomains discovery          |
    | `subfinder -d target.net`                                             | Passive subdomain enumeration |

???+ tip "vhost Enumeration"
    | Commands                                                                   | Description     |
    |----------------------------------------------------------------------------|-----------------|
    | `gobuster vhost -u https://target.net -w  ~/wordlists/vhosts-wordlist.txt` | Vhost discovery |

Small and compact webserver with python standard library

> `python3 -m http.server 80`
