# Apache webserver

## Installation & Management

???+ info "CLI"

    === "Debian/Ubuntu"
        **Installation**
        ```bash
        sudo apt install -y apache2
        sudo systemctl enable apache2
        sudo systemctl start apache2
        ```

        **UFW**
        ```bash
        ufw allow http
        ufw allow https
        ufw enable
        ```

    === "CentOS/RedHat/Rocky/Alma"
        **Installation**
        ```bash
        sudo dnf install -y httpd
        sudo systemctl enable httpd
        sudo systemctl start httpd
        ```

        **Firewall**
        ```bash
        firewall-cmd --zone=public --add-service=http --permanent
        firewall-cmd --zone=public --add-service=https --permanent
        firewall-cmd --reload
        ```

## Webserver

Configuration folder
`/etc/apache2`

| Files | Description |
| --- | --- |
| `/etc/apache2`   | Rename or New |
| `/etc/apache2`   | Rename or New |

Website files path `/var/www/html`

## Reverse-proxy

> ToDo

## Htaccess

> ToDo
