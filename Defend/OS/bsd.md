# BSD

**B**erkley **S**oftware **D**istribution (BSD) is a UNIX-like system used as base OS for firewall distributions like [pfsense](https://www.pfsense.org/) or [OPNsens](https://opnsense.org/).

???+ faq "Search"
    | Command            | Description            |
    |--------------------|------------------------|
    | `logins -a`        | List user with details |
    | `logins -l [user]` | Get user details       |

???+ failure "Lock users"
    | Command                            | Description     |
    |------------------------------------|-----------------|
    | `pw lock [user]`                   | Lock user       |
    | `chsh -s /usr/sbin/nologin [user]` | Lock user shell |
    | `pw unlock [user]`                 | Unlock user     |

???+ tldr "Manage users"
    | Command                               | Description                     |
    |---------------------------------------|---------------------------------|
    | `pw useradd -n [user] -s /bin/csh`    | Adding user                     |
    | `pw useradd -n [user] -s /bin/csh -m` | Adding user with home directory |
    | `passwd [user]`                       | Change user password            |
    | `pw userdel [user]`                   | Delete user                     |
    | `pw userdel [user] -r`                | Delete user and home directory  |

## Importants files

| Files                | Description                       |
|----------------------|-----------------------------------|
| `/etc/master.passwd` | Textual database for admins users |
| `/etc/passwd`        | Textual database for normal users |
