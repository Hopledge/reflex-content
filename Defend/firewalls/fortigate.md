# Fortigate

> [Documentation](https://docs.fortinet.com/document/fortigate/7.2.3/administration-guide/954635/getting-started)

### Installation

1. Connext with remote console
2. Change the startup password
3. `execute formatlogdisk` format the disk for logs (Init)
**Admin Port**
1. `config system interface` enter inside configuration menu for interfaces
2. `edit port6` enter in edit menu for admin port
3. `set ip x.x.x.x mask.mask.mask.mask` change ip adress
4. `set allowaccess ping http https ssh` allow network trafic
5. `end` quit menu
**Access to outside**
1. `config system interface` enter inside configuration menu for interfaces
2. `edit port1`  enter in edit menu for admin port
3. `set ip x.x.x.x mask.mask.mask.mask` change ip adress
4. `set allowaccess ping` allow network trafic
5. `end` quit menu
**Default gateway**
1. `config router static` enter inside configuration menu for gateway
2. `Edit 1` edit entry 1
3. `Set dst 0.0.0.0 0.0.0.0` edit destination adress
4. `Set device port1` edit port
5. `Set gateway x.x.x.x` edit gateway
6. `End` quit menu
**DNS server**
1. `Config system dns` enter inside configuration menu for DNS
2. `Set primary x.x.x.x` edit IP adress
3. `end` quit menu
**Add licence**
1. Configure administration station to get access to fortigate
2. Use web interface `https://<ip>`
3. Follow setup
