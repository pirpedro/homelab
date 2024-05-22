FROM arm64v8/ubuntu:20.04

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
 && apt-get install -y sudo avahi-daemon git

RUN adduser --disabled-password --gecos '' wirepod \
 && adduser wirepod sudo \
 && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER wirepod

RUN mkdir /home/wirepod/wire-pod \
 && cd /home/wirepod/wire-pod \
 && git clone https://github.com/kercre123/wire-pod.git .

WORKDIR /home/wirepod/wire-pod

RUN sudo STT=vosk ./setup.sh
CMD sudo ./chipper/start.sh
