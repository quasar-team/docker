FROM docker.cern.ch/linuxsupport/cc7-base:latest 

RUN yum --assumeyes update && yum install --assumeyes \
 wget \
 gcc-c++ \
 git \
 make \
 cmake \
 xsd \
 java-1.8.0-openjdk \
 libxml2-devel \
 xerces-c-devel \
 openssl-devel \
 pysvn \
 python-lxml

# special! astyle, use homemade rpm rather than building it from source
RUN wget https://cernbox.cern.ch/index.php/s/QfjnCb0mtVuSlJ2/download -O astyle.rpm && yum install --assumeyes astyle.rpm

#
# tidy up...
#
RUN yum clean all

ADD boost_1_59_0_build.tar.gz /3rdPartySoftware/BoostBuild
ADD unified_automation_1_1_3_build.tar.gz /3rdPartySoftware/UAToolkitBuild

ENV BOOST_HOME=/3rdPartySoftware/BoostBuild
ENV UNIFIED_AUTOMATION_HOME=/3rdPartySoftware/UAToolkitBuild
