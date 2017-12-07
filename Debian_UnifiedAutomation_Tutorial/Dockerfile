#FROM docker.io/ubuntu:16.10 
FROM alexismp/debian-openjdk

MAINTAINER Quasar Development Team (https://github.com/quasar-team)

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update \
&& apt-get install -y \
 build-essential \
 cmake \
 git \
 graphviz \
 astyle \
 libxml2-utils \
 xsdcxx \
 python-lxml \
 python-svn \
 libxml2-dev \
 libxerces-c-dev \
 libboost-filesystem-dev \
 libboost-all-dev \
 libssl-dev \
&& apt-get clean all

ENV BOOST_LIBS="-lssl -lcrypto -lboost_thread -lboost_program_options -lboost_system"


ENV OPCUA_TOOLKIT_PATH=/opt/OpcUaToolkit-1.3.3/sdk
ENV BOOST_HOME=/usr/include/boost
ENV BOOST_PATH_HEADERS=/usr/include/boost
ENV BOOST_PATH_LIBS=/usr/lib/x86_64-linux-gnu

RUN cd / \
   && git clone https://github.com/quasar-team/quasar.git \ 
   && cd quasar \
   && python quasar.py create_project demo/quasar 

ADD Design.xml /quasar/demo/quasar/Design/
ADD config.xml /quasar/demo/quasar/bin/
ADD ServerConfig.xml /quasar/demo/quasar/bin/
ADD uasdkcppbundle-bin-EVAL-debian7.tar.gz /opt/OpcUaToolkit-1.3.3

  
 RUN cd /quasar/demo/quasar \
   && python quasar.py set_build_config ../../FrameworkInternals/default_configuration.cmake \
   && ./quasar.py build  


WORKDIR /quasar/demo/quasar/bin


EXPOSE 4841


CMD ./OpcUaServer
