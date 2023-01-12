# SMB

Port : `445`

## SMB-Client

List shares

```bash
smbclient --no-pass //$TARGET -L
```

List files

```bash
smbclient --no-pass //$TARGET/$SHARE -c "ls"
# List folder
smbclient --no-pass //$TARGET/$SHARE -c "ls dir/"
```

Download file

```bash
smbclient --no-pass //$TARGET/$SHARE -c "get file.txt local_file.txt"
```

Connect to a server with username

```bash
smbclient //$TARGET/$SHARE -U <username>
```

Interactive mode

```bash
smbclient --no-pass //$TARGET/$SHARE -I"
```

## Sources

- [Hacking Windows shares from Linux with Samba](https://www.madirish.net/59)
