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
 default-jre \
 python3-jinja2 \
 python3-colorama \
 python3-lxml \
 python-svn \
 libxml2-dev \
 libxerces-c-dev \
 libboost-all-dev \
 libssl-dev \
 && apt-get clean all

RUN ln -s /usr/bin/cmake /usr/bin/cmake3 && \
 git config --global user.email quasar-developers@cern.ch && \
 git config --global user.name QuasarDeveloper

ENV BOOST_LIBS="-lboost_thread -lboost_system -lboost_program_options -lboost_system"
