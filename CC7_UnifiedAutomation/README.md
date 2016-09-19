# CERN Centos 7 image
This docker file creates a CERN Centos 7 docker image with dependencies loaded for building a quasar server using a Unified Automation backend (v1.3.3) built from source and boost v1.59 (also built from source) with the default namespace name mapped from "boost" to "boost_1_59_0". Note that the image built from this docker file is a *private* image; it must *not* be circulated outwith the pool of developers with a valid Unified Automation license. 

In order to build an image from this file, the developer must supply both a (zipped) Unified Automation toolkit install build and a boost build.
