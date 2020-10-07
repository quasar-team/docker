# Ubuntu quasar image
This docker file creates an Ubuntu docker image with dependencies loaded for the quasar quasar framework. Note that the image does not supply any OPC-UA back-end. Users of images built from this dockerfile wanting to build quasar servers will have to supply a back-end at build-time, for example the open source open62541 back-end (see open62541.org for details). The open62541 back-end can be integrated via the quasar optional module open62541-compat.

This is the dockerfile used to generate the image used in quasar linux CI. The linux CI image is stored in dockerhub (obtained via docker pull bfarnham/quasar:quasar-open62541).

Linux CI builds of quasar master branch run on tag 'quasar-open62541', therefore any potential changes to the image (pushed to dockerhub) should be tagged with 'quasar-open62541-next' to maintain separation of current and pending images. When image changes are complete, and satisfy linux CI requirements, the new image should be retagged to quasar-open62541, to ensure CI linux builds run on this tag.
