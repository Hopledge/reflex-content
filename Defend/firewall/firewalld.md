# FirewallD

???+ tip "Check firewall status"

    ```bash
    firewall-cmd --state
    ```

???+ info "Open ports"

    === "Custom"

        ```bash
        firewall-cmd --add-port=<port>/<protocol>  --permanent # (1)
        firewall-cmd --add-port=<portFrom>-<portTo>/<protocol> --permanent # (2)
        firewall-cmd --reload # (3)
        ```

        1. One port
        2. Range ports
        3. Reload firewalld config

    === "SSH"
        ```bash
        firewall-cmd --zone=public --add-service=ssh --permanent
        firewall-cmd --reload
        ```

    === "HTTP/HTTPS"
        ```bash
        firewall-cmd --zone=public --add-service=http --permanent
        firewall-cmd --zone=public --add-service=https --permanent
        firewall-cmd --reload
        ```

## Sources

- [How To Set Up a Firewall Using FirewallD on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7)
