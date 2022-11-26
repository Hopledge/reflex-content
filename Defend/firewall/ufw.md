
# UFW

Uncomplicated firewall build on the top of `iptables`

???+ tip "Status"
    | Command       | Description                                   |
    | ------------- | --------------------------------------------- |
    | `ufw enable`  | Enable the firewall                           |
    | `ufw disable` | Disable the firewall                          |
    | `ufw reload`  | Reload the firewall config after change rules |

???+ success "Create rules"
    | Command                                         | Description              |
    | ----------------------------------------------- | ------------------------ |
    | `ufw allow [port]/[protocol]`                   | Allow a port             |
    | `ufw allow from [subnet] to [type] port [port]` | Allow port from a subnet |
    | `ufw deny [port]/[protocol]`                    | Deny a port              |
    | `ufw deny in on [interface] from [IP]`          | Deny packets from an IP  |

???+ failure "Delete rules"
    | Command               | Description          |
    | --------------------- | -------------------- |
    | `ufw status numbered` | List rules with id   |
    | `ufw delete [id]`     | Delete rules with id |
