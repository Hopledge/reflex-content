# Linux

## User management

???+ faq "Commands"

    === "Search"
        | Command            | Description                                    |
        |--------------------|------------------------------------------------|
        | `w`                | Shows all logged users and what they are doing |
        | `logins -a`        | List user with details                         |
        | `logins -l [user]` | Get user details                               |

    === "Lock users"
        | Command                           | Description                   |
        |-----------------------------------|-------------------------------|
        | `passwd --status [user]`          | Check user lock status        |
        | `chage -l root [user]`            | Check user expire status      |
        | `chage -E0  [user]`               | Lock user by expiring account |
        | `usermod -s /sbin/nologin [user]` | Lock user shell               |

    === "Manage users"
        | Command             | Description                     |
        |---------------------|---------------------------------|
        | `id [user`          | Check user id                   |
        | `useradd [user]`    | Adding user                     |
        | `useradd -m [user]` | Adding user with home directory |
        | `passwd [user]`     | Change user password            |
        | `userdel [user]`    | Delete user                     |
        | `userdel -r [user]` | Delete user and home directory  |

## Importants files

| Files         | Description                       |
|---------------|-----------------------------------|
| `/etc/shadow` | Textual database for admins users |
| `/etc/passwd` | Textual database for normal users |
