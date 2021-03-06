#
# ==Purpose of the image created from this dockerfile==
# Provides an image for building quasar created OPC-UA servers from source
# using the Unified Automation backend.
#
# NOTE: Unified Automation is a *commercial* SDK, and this image is created
# with a build of the full (i.e. paid-for) SDK. Therefore this image
# MUST *NOT* BE MADE PUBLICLY AVAILABLE: Only SDK license holders may use it
#

FROM gitlab-registry.cern.ch/linuxsupport/cc7-base

MAINTAINER Quasar Development Team (http://github.com/quasar-team)

ADD libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm /tmp/

RUN yum clean expire-cache \ 
&& yum --assumeyes update && yum install --assumeyes \
     wget \
     gcc-c++ \
     git \
     make \
     cmake3 \
     ninja-build \
     xsd \
     astyle \
     java-1.8.0-openjdk \
     libxml2-devel \
     xerces-c-devel \
     openssl-devel \
     pysvn \
     python-lxml \
     python2-pip \
     rpm-build \
     qt-devel \
     /tmp/libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm \
     doxygen \
     graphviz \
     net-snmp \
     net-snmp-devel \
     vim \
     texlive texlive-xtab texlive-multirow texlive-sectsty texlive-tocloft texmaker \
     qt5-qtbase-devel qt5-qtserialport-devel \
&& ln -s /usr/bin/cmake3 /usr/bin/cmake \
&& ln -s /usr/bin/cpack3 /usr/bin/cpack \
&& pip install --upgrade pip \
&& pip install enum34 \
&& pip install six \
&& pip install pygit2==0.28.2 \
&& pip install jinja2 \
&& pip install colorama \
&& yum clean all

#
# Clean the 3rdPartySoftware directory, paranoid perhaps.
#
CMD rm-rf /3rdPartySoftware && mkdir /3rdPartySoftware

# 
# Copy uasdk source distro from docker build environment, ADD auto-extracts to /3rdPartySoftware/sdk/
# Build debug and release configurations, create static libs (then delete all source code etc)
# Set environment SDK variable 
#
ADD uasdkcppbundle-src-centos7.0-x86_64-gcc4.8.2-v1.5.6-361.tar.gz /3rdPartySoftware
ADD CERN_build_static_ua_stack.cmake /3rdPartySoftware/sdk/
RUN cd /3rdPartySoftware/sdk && \
  rm ./lib/* && \
  sh ./buildSdk.sh -t $(pwd)/CERN_build_static_ua_stack.cmake -c "Debug Release" && \
  find . -mindepth 1 -maxdepth 1 -type d -not -name include -not -name lib -not -name lic -exec rm -rf {} +
ENV UNIFIED_AUTOMATION_HOME=/3rdPartySoftware/sdk/

#
# Boost. Note we cannot use boost version distributed in epel repo. At time of writing
# it's too old (v1.48), we require boost Log: only introduced in 1.54.
# Copy zipped pre-built boost from docker build environment to  image
#
ADD boost_1_59_0.tar.gz /3rdPartySoftware
ADD boost_1_68_0.tar.gz /3rdPartySoftware
ENV BOOST_HOME=/3rdPartySoftware/boost_1_59_0/

#
# Anagate. Add dependencies from local zip file
# zip file obtained from http://www.anagate.de/en/support/download.htm - more info in README.md
#
ADD anagate-redistributables.tar.gz /3rdPartySoftware
