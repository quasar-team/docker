FROM docker.io/ubuntu:18.04

MAINTAINER Quasar Development Team (https://github.com/quasar-team)

RUN apt-get -y update && \
 apt-get install -y \
 build-essential \
 cmake \
 git \
 astyle \
 libxml2-utils \
 xsdcxx \
 python3-jinja2 \
 python3-colorama \
 python3-lxml \
 libxml2-dev \
 libxerces-c-dev \
 libboost-all-dev \
 libssl-dev \
 vim \
 && apt-get clean all

RUN ln -s /usr/bin/cmake /usr/bin/cmake3 && \
 git config --global user.email quasar-developers@cern.ch && \
 git config --global user.name QuasarDeveloper

ENV BOOST_LIBS="-lboost_thread -lboost_system -lboost_program_options -lboost_system"

RUN git clone https://github.com/quasar-team/UaSwissArmyKnife.git -b v0.5 \
  && cd UaSwissArmyKnife && bash build_linux_open62541.sh && cd build && make install

RUN cd /opt && git clone https://github.com/quasar-team/NodeSetTools.git -b v0.0.1
