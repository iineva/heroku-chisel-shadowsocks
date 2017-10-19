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
* Settings --> Config Variables --> set `SSPORT` `PASSWORD` and `METHOD` for shadowsocks server
* Done!

# Setup client

### open chisel client

```shell
chisel client https://your-herokuapp-identifier.herokuapp.com $LOCALPORT:$SSPORT
```
### config shadowsocks client

* host: localhost
* port: $LOCALPORT
* method: $METHOD
* password: $PASSWORD


# Setup client on docker (option)

* docker-compose.yml

```
version: "2"

services:
  chisel:
    image: jpillora/chisel
    restart: always
    ports:
      - "$LOCALPORT:$LOCALPORT"
    entrypoint: "chisel client https://your-herokuapp-identifier.herokuapp.com $LOCALPORT:$SSPORT"
```