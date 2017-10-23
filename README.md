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
* Deploy --> Deployment method --> Github --> choice `heroku-chisel-shadowsocks `
* Settings --> Config Variables --> set `PASSWORD` and `METHOD` for shadowsocks server
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

# Config shadowsocks client

* host: localhost (or your cloud host)
* port: $LOCALPORT (or your cloud host port)
* method: $METHOD
* password: $PASSWORD
