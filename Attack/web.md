# Web

???+ tip "DNS Enumeration"
    | Commands                                                           | Description                   |
    |--------------------------------------------------------------------|-------------------------------|
    | `gobuster dns -d $TARGET -w ~/wordlists/subdomains.txt --wildcard` | Subdomains discovery          |
    | `subfinder -d $TARGET`                                             | Passive subdomain enumeration |

???+ tip "vhost Enumeration"
    | Commands                                                                | Description     |
    |-------------------------------------------------------------------------|-----------------|
    | `gobuster vhost -u https://$TARGET -w  ~/wordlists/vhosts-wordlist.txt` | Vhost discovery |

Small and compact webserver with python standard library

> `python3 -m http.server 80`
