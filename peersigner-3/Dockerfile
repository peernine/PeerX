#signer-505
FROM ubuntu:xenial

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
ADD signer-505.json /signer.json
ADD signer.pass /signer.pass 

#<-- 55five 여기부턴 init -->
RUN geth --cache 512 init genesis.json
RUN echo mkdir -p /root/.ethereum/keystore/
RUN cp /signer.json /root/.ethereum/keystore/

#환경변수 설정
ENV address="0x5054db3275fde21e93b5d99f81f4d4a215366730"
ENV bootnodeId="9d6b515151c990c294e71dd1526e08968c7df360d21f8095ec945f9ff5454734f198d670c6b63f20796dde702dc1d8e18c92298df6a27c4424ace0b7bb174bd7"
ENV bootnodeIp="172.25.0.105"

#여기서 실행
CMD exec geth --networkid 13525 --verbosity=4 --rpc --rpcapi "eth,web3,personal,net,miner,admin,debug,db" --rpcaddr "0.0.0.0" --rpccorsdomain "*" --syncmode=full --cache 512 --port 30301 --nat extip:0.0.0.0 --maxpeers 50 --bootnodes "enode://$bootnodeId@$bootnodeIp:30301" --ethstats='peernine-signer-3:peerpass@localhost:3000' --etherbase $address --unlock $address --password /signer.pass --gasprice "0" --mine

EXPOSE 8545
EXPOSE 30303