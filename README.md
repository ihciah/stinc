# stinc
`shadowsocks` + `tinc` + `chnroute` in docker


![Docker Build Status](https://img.shields.io/docker/build/ihciah/stinc.svg)![Docker Automated build](https://img.shields.io/docker/automated/ihciah/stinc.svg)![Docker Stars](https://img.shields.io/docker/stars/ihciah/stinc.svg)![Docker Pulls](https://img.shields.io/docker/pulls/ihciah/stinc.svg)![Layers](https://images.microbadger.com/badges/image/ihciah/stinc.svg)


This project is designed to run a `shadowsocks` forwarding server simply. 

This docker runs on a server inside of China or a company, and it provides a `shadowsocks` proxy server for users. If user requests' destination IP is outside of China(not on the `chnroute` list), the packet will be forwarded to a server outside China through a tunnel, which is setup using `Tinc`.

To run this code, you need two servers: one inside, one outside. Setup a `tinc` node on outside server, and put inside node's configure file in `stinc/tinc_conf`. Then you should change `shadowsocks` configuration in `stinc/supervisor/conf.d`. 

Run directly in folder `stinc`: 
```
docker run --device=/dev/net/tun -v `pwd`/supervisor:/etc/supervisor -v `pwd`/tinc_conf:/etc/tinc -v `pwd`/dnsmasq.d:/etc/dnsmasq.d -p 10086:8388 -d --privileged ihciah/stinc
```

Or you can start it using `docker-compose` in folder `stinc`:
```
docker-compose up -d
```
