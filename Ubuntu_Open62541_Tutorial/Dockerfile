FROM docker.io/ubuntu:16.10 

MAINTAINER Quasar Development Team (https://github.com/quasar-team)


RUN apt-get -y update && \
 apt-get install -y \
 build-essential \
 cmake \
 git \
 graphviz \
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

RUN cd / \
   && git clone https://github.com/quasar-team/quasar.git \ 
   && cd quasar \
   && python quasar.py create_project demo/quasar 

ADD Design.xml /quasar/demo/quasar/Design/
ADD config.xml /quasar/demo/quasar/bin/
  
RUN cd /quasar/demo/quasar \
   && python quasar.py enable_module open62541-compat \
   && python quasar.py set_build_config ../../open62541_config.cmake \
   && python quasar.py prepare_build Release \
   && cd open62541-compat \
   && python prepare.py \
   && cd .. \
   && ./quasar.py build 




WORKDIR /quasar/demo/quasar/bin


EXPOSE 4841


CMD ./OpcUaServer
