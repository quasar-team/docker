# quasar UASDK Docker

## Author
Paris Moschovakos - paris@moschovakos.com

## Description
This directory, `quasar-uasdk`, contains a Dockerfile for building an image accompanied with a software stack suitable for the quasar team's Swiss Army Knife and NodeSetTools. The Docker image is based on the `cern/alma9-base` image, and has additional software installed to fulfill the dependencies of the quasar Team's tests.

## Dockerfile
The Dockerfile starts from the `cern/alma9-base` image, installs a range of dependencies including git, Python packages, CMake, gcc-c++, Boost, Graphviz, ninja, XML related tools, openssl, doxygen, astyle, and ends with pygit2. It also clones the quasar Team's UaSwissArmyKnife and NodeSetTools from their GitHub repositories.

The Dockerfile includes the following steps:

- Install basic dependencies
- Install Python dependencies
- Install CMake3 and GCC compiler
- Install Boost dependencies
- Install Graphviz for generating diagrams
- Install Ninja used as CMake generator
- Install XML related dependencies
- Install miscellaneous dependencies
- Install Doxygen for documentation generation
- Install Astyle for source code formatting
- Clean all cached information from DNF
- Install pygit2 using pip
- Copy sdk includes and libs into /opt/uasdk
- Clone and build UaSwissArmyKnife
- Clone NodeSetTools into /opt

Please refer to the Dockerfile for the specific details.

## License
This project is Copyright (C) 2023 Paris Moschovakos. All rights reserved.

