# stinc
Shadowsocks + tinc + chnroute in docker

Run: 
```
docker run --device=/dev/net/tun -v /home/ch/confs/supervisor:/etc/supervisor -v /home/ch/confs/tinc_conf:/etc/tinc -v /home/ch/confs/dnsmasq.d:/etc/dnsmasq.d -p 9999:8388 -d --privileged ihciah/stinc
```

Or you can run:
```
docker-compose up -d
```
