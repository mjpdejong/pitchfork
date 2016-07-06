# Pitchfork [![Build Status](https://travis-ci.org/PacificBiosciences/pitchfork.svg)](https://travis-ci.org/PacificBiosciences/pitchfork)
Prototyping github source building while having a dumb file (Makefile) to describe a software component.

    make init
    make blasr PREFIX=/opt/mybuild
    bash --init-file /opt/mybuild/setup-env.sh # either to use the build in the subshell
    source deployment/setup-env.sh             # or     to use the build in current sheel 

For more information, please visit the [wiki page](https://github.com/PacificBiosciences/pitchfork/wiki)
