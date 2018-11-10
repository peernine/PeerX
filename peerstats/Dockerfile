#peerstats
FROM peernine/ubuntu:16.04
MAINTAINER Alex Lee <alex.lee@peernine.co.kr>

ENV WS_SECRET peerpass
ENV PORT 3000

# -----------------------------------------------------------------------------
# git
RUN apt-fast update -y \
	&& apt-fast install -y git \
	&& apt-fast install -y sudo

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash - \
	&& sudo apt-get install nodejs


## # -----------------------------------------------------------------------------
## # intelligence 다운로드
## RUN git clone https://github.com/cubedro/eth-net-intelligence-api

## WORKDIR /home/peernine/eth-net-intelligence-api

## # ADD app.js /home/peernine/eth-net-intelligence-api/app.js
## ADD app.json /home/peernine/eth-net-intelligence-api/app.json

## RUN sudo npm install
## RUN sudo npm install -g pm2
## #RUN sudo npm install -g chalk
## CMD exec pm2 start app.json

# -----------------------------------------------------------------------------
# move
WORKDIR /home/peernine

# -----------------------------------------------------------------------------
# eth-netstats 다운로드
#RUN git clone https://github.com/cubedro/eth-netstats
RUN git clone https://github.com/puppeth/eth-netstats.git

WORKDIR /home/peernine/eth-netstats

RUN npm install
RUN sudo npm install -g grunt-cli
RUN grunt

CMD ["npm start"]
