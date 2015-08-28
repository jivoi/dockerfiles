# run a tor in a container
#
#
FROM alpine:latest
MAINTAINER EK <ekoz@protonmail.com>

# Note: Tor is only in testing repo -> http://pkgs.alpinelinux.org/packages?package=emacs&repo=all&arch=x86_64
RUN apk update && apk add \
	tor \
	--update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ \
	&& rm -rf /var/cache/apk/*

# default port to used for incoming Tor connections
# can be changed in torrc
EXPOSE 9050

# copy in our torrc files
COPY torrc.socks5 /etc/tor/torrc.socks5

# make sure files are owned by tor user
RUN chown -R tor /etc/tor

USER tor

ENTRYPOINT [ "tor" ]
