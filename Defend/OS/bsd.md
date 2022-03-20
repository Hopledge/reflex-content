# BSD

**B**erkley **S**oftware **D**istribution (BSD) is a UNIX-like system used as base OS for firewall distributions like [pfsense](https://www.pfsense.org/) or [**OPNsens**](https://opnsense.org/).

???+ failure "Manage users"
    | Command                               | Description                     |
    | ------------------------------------- | ------------------------------- |
    | `pw lock [user]`                      | Lock user                       |
    | `pw unlock [user]`                    | Unlock user                     |
    | `chsh -s /usr/sbin/nologin [user]`    | Disable user login              |
    | `passwd [user]`                       | Change user password            |
    | `pw useradd -n [user] -s /bin/csh`    | Adding user                     |
    | `pw useradd -n [user] -s /bin/csh -m` | Adding user with home directory |
    | `pw userdel [user]`                   | Delete user                     |
    | `pw userdel [user] -r`                | Delete user and home directory  |
