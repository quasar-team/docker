# CERN Centos 7 image
This docker file creates a CERN Centos 7 docker image with dependencies loaded for building a quasar server using a Unified Automation backend (v1.3.3) built from source and boost v1.59 (also built from source) with the default namespace name mapped from "boost" to "boost_1_59_0". Note that the image built from this docker file is a *private* image; it must *not* be circulated outwith the pool of developers with a valid Unified Automation license. 

In order to build an image from this file, the developer must supply both a (zipped) Unified Automation toolkit install build and a boost build.

Contents of the directory from which this docker image is built  
.  
├── boost_1_59_0.tar.gz  
├── boost_1_68_0.tar.gz  
├── CERN_build_static_ua_stack.cmake  
├── Dockerfile  
├── libsocketcan-devel-0.0.9-p0.cc7.x86_64.rpm  
├── README.md  
├── uasdkcppbundle-src-centos7.0-x86_64-gcc4.8.2-v1.5.6-361.tar.gz
└── anagate-redistributables.tar.gz (obtained from http://www.anagate.de/download/API/AnaGateAPI-CAN-1.11-2.13.tar.bz2)

Note that the anagate-redistributables.tar.gz has been 'treated' to keep the size minimal. This just means that the original archive was downloaded
from the URL above, then all unneccesary contents removed (arm binaries, 32 bit binaries, static libs (\*.a - cannot use these since they're not
compiled with fPIC). This is just to keep the size to a minimum. Once the trash is stripped out - the resulting directory is just compressed again
with 'tar'

