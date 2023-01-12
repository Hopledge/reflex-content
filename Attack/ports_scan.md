# Ports scan

???+ tip "Nmap quick win"
    | Commands                                | Description      |
    |-----------------------------------------|------------------|
    | `nmap 192.168.1.1/24 -sn`               | Host discovery   |
    | `sudo nmap -sSVC -O -T4 192.168.1.1`    | TCP Scan ++      |
    | `sudo nmap -sSVC -O -f -T1 192.168.1.1` | TCP Scan stealth |

???+ tip "Nmap flags"
    | Flags         | Description                   |
    |---------------|-------------------------------|
    | `-sS`         | TCP SYN                       |
    | `-sT`         | TCP Connect                   |
    | `-sA`         | TCP ACK                       |
    | `-sN,-sF,-sX` | TCP NULL, FIN, XMAS           |
    | `-sU`         | UDP (Slow)                    |
    | `-sV`         | Detect versions               |
    | `-O`          | OS Fingerprinting             |
    | `-f`          | Fragment packets              |
    | `-p 0-1024`   | Ports range                   |
    | `-T0`         | Aggressivity (0 to 5)         |
    | `-Pn`         | Skip host discovery           |
    | `-iL`         | Using input target from files |
