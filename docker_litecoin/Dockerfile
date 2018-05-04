FROM ubuntu:14.04

MAINTAINER Michael Lehman <mjlehman99@gmail.com>

EXPOSE 9332/tcp 9333/tcp

RUN echo "deb http://ppa.launchpad.net/bitcoin/bitcoin/ubuntu trusty main" > /etc/apt/sources.list.d/bitcoin-bitcoin-trusty.list
RUN mkdir /opt/litecoin && apt-get update && apt-get install -y \
	libboost-system-dev \
	libboost-program-options-dev \
	libboost-thread-dev \
	libminiupnpc-dev \
	libevent-dev \
	libboost-filesystem-dev 
RUN apt-get install --yes --force-yes \
	libdb4.8-dev \
	libdb4.8++-dev
ADD litecoind /opt/litecoin/litecoind

ENTRYPOINT ["/opt/litecoin/litecoind"]


