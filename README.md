# stinc
Shadowsocks + tinc + chnroute in docker

Docker build and then run `docker run --device=/dev/net/tun -v /home/ch/confs/supervisor:/etc/supervisor -v /home/ch/confs/tinc_conf:/etc/tinc -v /home/ch/confs/dnsmasq.d:/etc/dnsmasq.d -p 9999:8388 -d --privileged stinc`, or you can write your own docker-compose
