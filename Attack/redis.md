# Redis

Port : `6379`

## Redis-Cli

Ping database

```bash
redis-cli -h $TARGET -p 6379 PING
```

Connect to database

```bash
redis-cli -h $TARGET -p 6379
# With password
redis-cli -h $TARGET -p 6379 -a
```

List all keys

```bash
redis-cli -h $TARGET -p 6379 --scan
```

> For security reasons, provide the password to redis-cli automatically via the REDISCLI_AUTH environment variable.

???+ tip "CLI commands"

    | Commands       | Description                                |
    |----------------|--------------------------------------------|
    | `get key_name` | Retrieve key value                         |
    | `keys *`       | List all keys                              |
    | `info`         | Retrieve informations about redis instance |
