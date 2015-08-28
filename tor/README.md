### BUILD
docker build -t=tor-socks5 .

### RUN
docker run -d -v /etc/localtime:/etc/localtime --restart always -p 9050:9050 --name tor tor-socks5 -f /etc/tor/torrc.socks5
