FROM ubuntu:18.04
RUN apt-get update && apt-get install -y \
  g++ \
  git \
  python3 \
  python3-lxml \
  python3-jinja2 \
  python3-colorama \
  cmake \
  libboost-all-dev \
  libxml2-utils \
  xsdcxx \
  astyle \
  libxerces-c-dev \
  libssl-dev \
  libxml2-dev \
  vim \
  && update-alternatives --install /usr/bin/python python /usr/bin/python3 10
COPY sdk/include /opt/uasdk/include
COPY sdk/lib /opt/uasdk/lib

RUN git clone https://github.com/quasar-team/UaSwissArmyKnife.git -b v0.4 \
  && cd UaSwissArmyKnife && bash build_linux_open62541.sh && cd build && make install
