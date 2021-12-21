# sonic-builder
Automating local sonic builds

## Requirements
multipass installed
A host with enough CPU/RAM/disk (16 GB RAM, 300GB free disk space)

## Instructions

Use the `sonic-cloud-init.yaml` file as a cloud-init script.
It will setup docker and all the other tedious things needed to build sonic for you.
You'll be left with a machine ready to build. 
Assumes you are using Ubuntu, probably won't work otherwise.

To use this with e.g. multipass, do this:
- `git clone https://github.com/antongisli/sonic-builder.git`
- `multipass launch 20.04 -n sonic-builder -c8 -m10G -d300G --cloud-init sonic-cloud-init.yaml`
- Log in: `multipass shell sonic-builder`

Docker vs build scripts are made for you in home dir, one to build arm one x86. 
Note that you may want to edit these to checkout a different version of sonic, since
sometimes builds just don't work otherwise. By default, the scripts use the master branch.
- `build-vs-arm-docker.sh`
- `build-vs-docker.sh`

Now pray to the Gods above, and perhaps you will end up with a working docker image :).

Notes on using the docker images:
~/sonic-buildimage/platform/vs/README.vsdocker.md 
