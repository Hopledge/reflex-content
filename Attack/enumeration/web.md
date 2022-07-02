# Web

???+ tip "Gobuster enumeration domain"
    | Commands                                | Description      |
    | --------------------------------------- | ---------------- |
    | `gobuster vhost -u https://target.net -w  ~/wordlists/vhosts-wordlist.txt`               | Vhost discovery   |
    | `gobuster dns -d target.net -w ~/wordlists/subdomains.txt --wildcard`               | Subdomains discovery   |
