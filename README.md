# heroku-chisel-shadowsocks

shadowsocks server over chisel

# Dependent

* [Shadowsocks](https://github.com/shadowsocks/shadowsocks/tree/master)
* [Chisel](https://github.com/jpillora/chisel)

# Data flow

`user request` <--> `shadowsocks client` <--> `chisel client` <--> `chisel server` <--> `shadowsocks server` <--> `target website`

# Setup Heroku Server

* Fork this repository
* Login to heroku --> Create new app
* `Deploy` --> `Deployment method` --> `Github` --> choice `heroku-chisel-shadowsocks `
* `Deploy` --> `Manual deploy` --> Select `master` branch --> `Depoly Branch`
* Open `https://<your-herokuapp-identifier>.herokuapp.com` in browser, if you see `Not found`, Done!

# Setup chisel client

```shell
chisel client https://<your-herokuapp-identifier>.herokuapp.com $LOCALPORT:8888
```

# Setup chisel client on docker (option)

* docker-compose.yml

```
version: "2"

services:
  chisel:
    image: jpillora/chisel
    restart: always
    ports:
      - "$LOCALPORT:8888"
    entrypoint: "chisel client --keepalive=2m https://<your-herokuapp-identifier>.herokuapp.com 8888:8888"
```

# Change shadowsocks `Server port` `Method` `Password` (option)

* Available methods: AEAD_AES_128_GCM AEAD_AES_192_GCM AEAD_AES_256_GCM AEAD_CHACHA20_POLY1305(CHACHA20-IETF-POLY1305) AES-128-CFB AES-128-CTR AES-192-CFB AES-192-CTR AES-256-CFB AES-256-CTR CHACHA20-IETF XCHACHA20

Key | Default | Info
---- | ---- | ----
SSPORT | 8888 | shadowsocks server port behind heroku
METHOD | CHACHA20-IETF-POLY1305 | encryption method
PASSWORD | steven | password

* Login to heroku --> Settings --> Config Variables --> set `SSPORT` `METHOD` `PASSWORD`
* `Deploy` --> `Manual deploy` --> Select `master` branch --> `Depoly Branch`

# Config shadowsocks client

* Host: `localhost` (or your cloud host)
* Port: `$LOCALPORT` (or your cloud host port)
* Method: `CHACHA20-IETF-POLY1305`
* Password: `steven`
