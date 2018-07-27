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
 python-lxml \
 python-svn \
 libxml2-dev \
 libxerces-c-dev \
 libboost-all-dev \
 libssl-dev \
 && apt-get clean all

ENV BOOST_LIBS="-lboost_thread -lboost_system -lboost_program_options -lboost_system"
