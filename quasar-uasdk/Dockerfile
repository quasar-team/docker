# Copyright (C) 2023 Paris Moschovakos <paris@moschovakos.com>

FROM cern/alma9-base

LABEL Paris Moschovakos

RUN dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
#
# Update dependancies
#
RUN dnf install -y \

#
#	Install basic dependencies
#
    git \
    patch \

#
#	Install python dependencies
#
#  python3 \
  python3-colorama \
  python3-jinja2 \
  python3-lxml \
  python3-pip \

#
# Install CMake3
#
  cmake3 \

#
# Install compiler
#
  gcc-c++ \

#
#	Install boost dependencies
#
  boost-devel \

#
# Install graphviz for generating diagrams
#
  graphviz \

#
# Install ninja used as CMake generator
#
  ninja-build \

#
# Install XML related dependancies
#
  xsd \
  xerces-c-devel \
  libxml2-devel \

#
# Install misc dependancies (hashing etc)
#
  openssl-devel \

#
# Install doxygen for documentation generation
#
  doxygen \

#
# Install astyle for source code formatting
#
  astyle \


# Clean all cached information
  && dnf clean all \

#
# Install pygit2
#
  && python3 -m pip install pygit2

COPY sdk/include /opt/uasdk/include
COPY sdk/lib /opt/uasdk/lib

RUN git clone https://github.com/quasar-team/UaSwissArmyKnife.git -b v0.7 \
  && cd UaSwissArmyKnife && bash build_linux_open62541.sh && cd build && make install

RUN cd /opt && git clone https://github.com/quasar-team/NodeSetTools.git -b v0.0.5
