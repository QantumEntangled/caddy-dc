# Caddy Docker-Compose Server

Docker-Compose configuration for Caddy

## Setup

Edit the `Caddyfile` with the destination names of the sites it will handle.

## Start Server

To start server run the following command:

```Bash
docker-compose up -d
```

## Restart Server

The server will need restarted after updating the `Caddyfile` by running the following command:

```Bash
docker-compose restart
```

## Example Caddyfile

```Caddyfile
site1.example.com {
    proxy / remote.server:80 {
        transparent
        websocket
    }
}

site2.example.com {
    root /www/site2/
    gzip
}

http://site3.example.com {
    root /www/site3/
    log /www/logs/site3-access.log
}

http://site4.example.com:8003, localhost:8003 {
    root /www/site4/

    basicauth / username1 password1
    basicauth / username2 password2

}
```

## Certificates

Caddy will automatically register SSL certificates with Let's Encrypt upon start for any domains without a URI specified or with `https` enabled. These certs are stored in the `/certs/` directory (will be created when the first cert is created).