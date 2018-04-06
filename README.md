# stinc
Shadowsocks + tinc + chnroute in docker



This project is designed to run a `shadowsocks` forwarding server simply. 

This docker runs on a server inside of China or a company, and it provides a `shadowsocks` proxy server for users. If user requests' destination IP is outside of China(not on the `chnroute` list), the packet will be forwarded to a server outside China through a tunnel, which is setup using `Tinc`.

To run this code, you need two servers: one inside, one outside. Setup a `tinc` node on outside server, and put inside node's configure file in `stinc/tinc_conf`. Then you should change `shadowsocks` configuration in `stinc/supervisor/conf.d`. 

Run directly: 
```
docker run --device=/dev/net/tun -v /home/ch/confs/supervisor:/etc/supervisor -v /home/ch/confs/tinc_conf:/etc/tinc -v /home/ch/confs/dnsmasq.d:/etc/dnsmasq.d -p 9999:8388 -d --privileged ihciah/stinc
```

Or you can start it using `docker-compose`:
```
docker-compose up -d
```
