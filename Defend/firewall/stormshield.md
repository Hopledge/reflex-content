# Stormshield

> [Global documentation](https://documentation.stormshield.eu/HOME/Content/Website_Topics/Root-HomePage-FR.htm)
> [CLI documentation](https://documentation.stormshield.eu/SNS/v4/fr/Content/PDF/SNS-TechnicalNotes/sns-fr-configuration_de_base_cli_note_technique.pdf)

## Informations

- [Adress by default](https://10.0.0.254/admin)

???+ info "CLI"

    === "Shell"
        | Command | Explainations                               |
        |---------|---------------------------------------------|
        |`defaultconfig -f -r`    |Reset firewall configuration |

    === "SRPClient"
        | Command | Explainations                         |
        |---------|---------------------------------------|
        |`cli`    |Launch **SRPClient** and start a shell |

## Backup/Restore

???+ info "CLI"

    === "Backup"
        ```bash
        CONFIG BACKUP list=all [password=<password>]> mybackup.na
        ```

    === "Restore"
        ```bash
        CONFIG RESTORE list=all [password=<password>]< mybackup.na
        ```

## Update firewall

```bash
SYSTEM UPDATE UPLOAD < file.maj
SYSTEM UPDATE ACTIVATE
```

## SSH

```bash
CONFIG CONSOLE SSH state=1 userpass=1 port=ssh
CONFIG CONSOLE ACTIVATE

CONFIG CONSOLE SSH state=0
CONFIG CONSOLE ACTIVATE
```

## Reflex

### Install SNS

**Setup**

1. Connect to the server with [adress](https://10.0.0.254/admin)
2. Edit interfaces
3. Edit the bridge to allow `in` and `out` available (Managing members)
4. Delete the bridge
5. Activate `out` interface
6. Edit `out` and change ip range
7. Edit `in` and change ip route
8. Apply changes
9. Change admin ethernet config
10. Login on https://<newIp>/admins
11. admin~>Gain write privilege
12. Configuration~>Objects~>Network Object
13. Create gateway object with IP
14. Create dns object with IP
15. In route, edit default gateway
16. Configuration, change DNS to dns object
17. Configuration, change NTP + Timezone
18. Configuration~>Network settings

### Filter and NAT

1. Create network object
2. Security policies~>New rules
