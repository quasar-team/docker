FROM docker.io/ubuntu:18.04 

MAINTAINER Quasar Development Team (https://github.com/quasar-team)

#
# libgit2 and pygit2 (see below). The weirdness about versions
# in the install stage stems from pygit versions being tightly
# bound to libgit2-dev versions. So, both fixed to v0.26.
#
RUN apt-get -y update \
 && apt-get install -y \
 build-essential \
 cmake \
 git \
 astyle \
 libxml2-utils \
 xsdcxx \
 default-jre \
 python-lxml \
 python-svn \
 python-pip \
 libxml2-dev \
 libxerces-c-dev \
 libboost-all-dev \
 libssl-dev \
 && python -m pip install --upgrade pip \
 && apt install -y libgit2-dev=0.26.0+dfsg.1-1.1ubuntu0.2 \
 && python -m pip install pygit2==0.26 \
 && python -m pip install enum34 \
 && apt-get clean all \
 && ln -s /usr/bin/cmake /usr/bin/cmake3 # use cmake3

ENV BOOST_LIBS="-lboost_thread -lboost_system -lboost_program_options -lboost_system"
