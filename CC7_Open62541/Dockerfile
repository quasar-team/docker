#
# ==Purpose of the image created from this dockerfile==
# Provides an image for building quasar created OPC-UA servers from source
# using the open62541 back-end
#
FROM gitlab-registry.cern.ch/linuxsupport/cc7-base

MAINTAINER Quasar Development Team (http://github.com/quasar-team)

ADD libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm /tmp/
ADD astyle-3.1-8.el7.cern.x86_64.rpm /tmp/

RUN yum clean expire-cache \ 
&&  yum --assumeyes update \
&&  yum install --assumeyes \
     wget \
     git \
     make \
     cmake3 \
     centos-release-scl \
     devtoolset-11 \
     ninja-build \
     xsd \
     astyle \
     libxml2-devel \
     xerces-c-devel \
     openssl-devel \
     openssl11-libs \
     python3 \
     /tmp/libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm \
     /tmp/astyle-3.1-8.el7.cern.x86_64.rpm \
     net-snmp \
     net-snmp-devel \
     vim \
&& yum clean all \
&& ln -sf /usr/bin/cmake3 /usr/bin/cmake \
&& ln -sf /usr/bin/python3 /usr/bin/python \
&& rm -rf /tmp/libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm \
&& rm -rf /tmp/astyle-3.1-8.el7.cern.x86_64.rpm \
&& rm -rf /3rdPartySoftware && mkdir /3rdPartySoftware

#
# create virtual python env, fill with required deps ( /python3_quasar_venv ). Activate venv to use
#
RUN python3 -m venv /python3_quasar_venv \
&&  source /python3_quasar_venv/bin/activate \
&&  python3 -m pip install --upgrade pip lxml jinja2 colorama pygit2==0.28.2

#
# Anagate. Add dependencies from local zip file
# zip file obtained from http://www.anagate.de/en/support/download.htm - more info in README.md
#
ADD anagate-redistributables.tar.gz /3rdPartySoftware

#
# Boost; use 1_81_0 (pre-built outside this image)
#
ADD boost_1_81_0.tar.gz /3rdPartySoftware
ENV BOOST_HOME=/3rdPartySoftware/boost_1_81_0

#
# Enable devtoolset
#
CMD source scl_source enable devtoolset-11
