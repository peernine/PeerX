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

# -----------------------------------------------------------------------------
# eth-netstats 다운로드
RUN git clone https://github.com/cubedro/eth-netstats

WORKDIR /home/peernine/eth-netstats

RUN npm install
RUN sudo npm install -g grunt-cli
#RUN sudo npm install grunt --save-dev
RUN ls
RUN grunt

CMD ["npm start"]
