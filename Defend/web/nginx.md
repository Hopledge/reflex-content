# Nginx

> ToDo

## Reverse-proxy

```yml
server { # simple reverse-proxy
    listen       80;
    server_name  domain2.com www.domain2.com;
    access_log   logs/domain2.access.log  main;

    # serve static files
    location ~ ^/(images|javascript|js|css|flash|media|static)/  {
      root    /var/www/virtual/big.server.com/htdocs;
      expires 30d;
    }

    # pass requests for dynamic content to rails/turbogears/zope, et al
    location / {
      proxy_pass      http://127.0.0.1:8080;
    }
  }
```

## Load balancing

```yml
upstream big_server_com {
    server 127.0.0.3:8000 weight=5;
    server 127.0.0.3:8001 weight=5;
    server 192.168.0.1:8000;
    server 192.168.0.1:8001;
  }

server { # simple load balancing
    listen          80;
    server_name     big.server.com;
    access_log      logs/big.server.access.log main;

    location / {
      proxy_pass      http://big_server_com;
    }
  }
```

## Security option

First install nginx plugin to get more option on nginx.
`sudo apt install nginx-extras`
This packet allow you tu use option like more_clear_headers Server

```
  server_tokens off;
  more_clear_headers Server;
  add_header X-Content-Type-Options nosniff;
  add_header X-Frame-Options "SAMEORIGIN";
  add_header X-Robots-Tag none;
  add_header X-Download-Options noopen;
  add_header X-Permitted-Cross-Domain-Policies none;
  add_header X-XSS-Protection "1; mode=block";
  add_header Referrer-Policy "strict-origin";
  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```

## Documentation

- [Nginx official documentation](https://www.nginx.com/resources/wiki/start/topics/examples/full/)
