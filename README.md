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
    entrypoint: "chisel client https://<your-herokuapp-identifier>.herokuapp.com 8888:8888"
```

# Change shadowsocks `Server port` `Method` `Password` (option)

Key | Default | Info
---- | ---- | ----
SSPORT | 8888 | shadowsocks server port behind heroku
METHOD | aes-256-cfb | encryption method
PASSWORD | steven | password

* Login to heroku --> Settings --> Config Variables --> set `SSPORT` `METHOD` `PASSWORD`
* `Deploy` --> `Manual deploy` --> Select `master` branch --> `Depoly Branch`

# Config shadowsocks client

* Host: `localhost` (or your cloud host)
* Port: `$LOCALPORT` (or your cloud host port)
* Method: `aes-256-cfb`
* Password: `steven`
