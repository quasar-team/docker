#
# ==Purpose of the image created from this dockerfile==
# Provides an image for building quasar created OPC-UA servers from source
# using the Unified Automation backend with gcc10 (uses cvmfs).
#
# NOTE: Unified Automation is a *commercial* SDK, and this image is created
# with a build of the full (i.e. paid-for) SDK. Therefore this image
# MUST *NOT* BE MADE PUBLICLY AVAILABLE: Only SDK license holders may use it
#
# image assumes host environment will have mounted and setup cvmfs (see 
# https://cernvm.cern.ch/fs/) and that the docker host shares its /cvmfs
# mount with this image.
#
# Something like this for the 'docker run' command executed on host
# docker run --privileged --interactive --tty --volume /cvmfs:/cvmfs <image> <cmd>
#
# then, gitlab-CI scripts should source the relevant LCG toolset, and 
# activate the python venv
# source /cvmfs/sft.cern.ch/lcg/releases/LCG_99/setuptools/44.1.0/x86_64-centos7-gcc10-opt/setuptools-env.sh
# source /python3_quasar_venv/bin/activate

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
     ninja-build \
     xsd \
     astyle \
     libxml2-devel \
     xerces-c-devel \
     openssl-devel \
     openssl11-libs \
     python3 \
     rpm-build \
     qt-devel \
     /tmp/libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm \
     /tmp/astyle-3.1-8.el7.cern.x86_64.rpm \
     doxygen \
     graphviz \
     net-snmp \
     net-snmp-devel \
     vim \
     texlive texlive-xtab texlive-multirow texlive-sectsty texlive-tocloft texmaker \
     qt5-qtbase-devel qt5-qtserialport-devel \
&& yum clean all \
&& ln -sf /usr/bin/cmake3 /usr/bin/cmake \
&& ln -sf /usr/bin/cpack3 /usr/bin/cpack \
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
# Copy pre-built uasdk distro from docker build environment, ADD to /3rdPartySoftware/sdk/
#
ADD sdk-1_6_5_x86_64-centos7-gcc10.tar.gz /3rdPartySoftware/
ENV UNIFIED_AUTOMATION_HOME=/3rdPartySoftware/sdk/

#
# Anagate. Add dependencies from local zip file
# zip file obtained from http://www.anagate.de/en/support/download.htm - more info in README.md
#
ADD anagate-redistributables.tar.gz /3rdPartySoftware

#
# Boost; use version in LCG_99 release
#
ENV BOOST_ROOT=/cvmfs/sft.cern.ch/lcg/releases/LCG_99/Boost/1.73.0/x86_64-centos7-gcc10-opt

#
# (runtime) activate g++10 (from cvmfs) and python venv
#
CMD source /cvmfs/sft.cern.ch/lcg/releases/LCG_99/setuptools/44.1.0/x86_64-centos7-gcc10-opt/setuptools-env.sh
CMD source /python3_quasar_venv/bin/activate
