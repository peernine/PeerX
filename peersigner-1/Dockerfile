#signer-1bb
FROM ubuntu:xenial
MAINTAINER Alex Lee <alex.lee@peernine.co.kr>

RUN apt-get update \
     && apt-get install -y wget software-properties-common \
     && rm -rf /var/lib/apt/lists/*

RUN add-apt-repository -y ppa:ethereum/ethereum

#55five
ARG binary
RUN apt-get update \
     && apt-get install -y ethereum=$binary

#55five
ARG signer.pass

RUN echo $signer.pass > /signer.pass

ADD genesis.json /genesis.json
ADD signer-1bb.json /signer.json
ADD signer.pass /signer.pass 

#<-- 55five 여기부턴 init -->
RUN geth --cache 512 init genesis.json
RUN echo mkdir -p /root/.ethereum/keystore/
RUN cp /signer.json /root/.ethereum/keystore/

#환경변수 설정
ENV address="0x1bb7a110f310934efecfbd88db409a73282c1cc1"
ENV bootnodeId="9d6b515151c990c294e71dd1526e08968c7df360d21f8095ec945f9ff5454734f198d670c6b63f20796dde702dc1d8e18c92298df6a27c4424ace0b7bb174bd7"
ENV bootnodeIp="172.25.0.105"

#여기서 실행
#--ethstats 'sealer1:peerpass@localhost:8080'
CMD exec geth --networkid 13525 --verbosity=4 --rpc --rpcapi "eth,web3,personal,net,miner,admin,debug,db" --rpcaddr "0.0.0.0" --rpccorsdomain "*" --syncmode=full --cache 512 --port 30301 --nat extip:127.0.0.1 --maxpeers 50 --bootnodes "enode://$bootnodeId@$bootnodeIp:30301" --ethstats='peernine-signer-1:peerpass@127.0.0.1:3000' --etherbase $address --unlock $address --password /signer.pass --gasprice "0" --mine

EXPOSE 8545
EXPOSE 30303