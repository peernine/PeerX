#peerstats
FROM peernine/ubuntu:16.04
MAINTAINER Alex Lee <alex.lee@peernine.co.kr>

ENV WS_SECRET peerpass
ENV PORT 3000

# -----------------------------------------------------------------------------
# git
RUN apt-get update -y \
	&& apt-get install -y git \
	&& apt-get install -y sudo

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash - \
	&& sudo apt-get install nodejs

# -----------------------------------------------------------------------------
# move
WORKDIR /home/peernine

# -----------------------------------------------------------------------------
# eth-netstats 다운로드
RUN git clone https://github.com/puppeth/eth-netstats.git

WORKDIR /home/peernine/eth-netstats

RUN npm install
RUN sudo npm install -g grunt-cli
RUN grunt

CMD ["npm start"]
