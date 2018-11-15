FROM ubuntu:xenial
MAINTAINER Alex Lee <alex.lee@peernine.co.kr>

RUN apt-get update \
     && apt-get install -y wget software-properties-common \
     && rm -rf /var/lib/apt/lists/*

# -----------------------------------------------------------------------------
# Run Upgrade
RUN apt-get update -y \
	&& apt-get -y upgrade \
	&& apt-get -o Dpkg::Options::=--force-confdef -y install curl netcat wget telnet vim bzip2 ssmtp locales python-pip software-properties-common python-software-properties bash-completion net-tools iputils-ping language-pack-ko apt-utils \
	&& locale-gen ko_KR.utf8 \
	&& localedef -i ko_KR -c -f UTF-8 -A /usr/share/locale/locale.alias ko_KR.UTF-8 \
	&& chmod -R 777 /var/run /var/log /etc/passwd /etc/group \
	&& pip --no-cache install --upgrade pip

# -----------------------------------------------------------------------------
# timezone Asia/Seoul
RUN apt-get install -y tzdata \
	&& ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime \
	&& echo "Asia/Seoul" > /etc/timezone \
	&& dpkg-reconfigure -f noninteractive tzdata

# -----------------------------------------------------------------------------
# add user peernine
RUN useradd -r -m peernine \
    && echo "peernine:123455" | chpasswd \
    && echo "root:123455" | chpasswd

WORKDIR "/home/peernine"

# -----------------------------------------------------------------------------
# Ensure UTF-8
ENV \
	LC_ALL=ko_KR.UTF-8 \
	LANG=ko_KR.UTF-8 \
	LANGUAGE=ko_KR.UTF-8

RUN add-apt-repository -y ppa:ethereum/ethereum

ARG binary
RUN apt-get update \
     && apt-get install -y ethereum=$binary

ENV nodekeyhex=""
CMD exec bootnode -nodekeyhex $nodekeyhex -verbosity 9 -addr $bootnodeIp:30301

EXPOSE 30301
EXPOSE 30301/udp

