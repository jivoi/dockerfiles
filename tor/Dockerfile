# run a tor in a container
#
#
#docker build -t=tor .
#
#docker run -d \
#    -v /etc/localtime:/etc/localtime \ # so time is synced
#    --restart always \ # why not?
#    -p 9050:9050 \ # expose/publish the port
#    --name tor-relay \
#    tor-relay -f /etc/tor/torrc.middle

FROM alpine:latest
MAINTAINER EK <ekoz@protonmail.com>

# Note: Tor is only in testing repo -> http://pkgs.alpinelinux.org/packages?package=emacs&repo=all&arch=x86_64
RUN apk update && apk add \
	tor \
	--update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ \
	&& rm -rf /var/cache/apk/*

# default port to used for incoming Tor connections
# can be changed by changing 'ORPort' in torrc
EXPOSE 9050

# copy in our torrc files
COPY torrc.middle /etc/tor/torrc.middle

# make sure files are owned by tor user
RUN chown -R tor /etc/tor

USER tor

ENTRYPOINT [ "tor" ]
