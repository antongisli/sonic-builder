# sonic-builder
Automating local sonic builds. Motivation for this is to use a sane environment without messing up your local machine.

Uses multipass to spawn Ubuntu VMs for building, and cloud-init to do all the tedious work of setting up the build env.

At the end, you have freedom to try the build in different ways, but there are two example scripts provided.

## Requirements
- multipass installed
- A host with enough CPU/RAM/disk (16 GB RAM, 300GB free disk space)
- Assumes you are using Ubuntu as a host, but has been tested and works on a windows host too.

## Instructions

Use the `sonic-cloud-init.yaml` file as a cloud-init script.
It will setup docker and all the other tedious things needed to build sonic for you.
You'll be left with a machine ready to build. 


To use this with multipass, do this:
- `git clone https://github.com/antongisli/sonic-builder.git`
- `multipass launch 20.04 -n sonic-builder -c8 -m10G -d300G --cloud-init sonic-builder/sonic-cloud-init.yaml`
- Log in: `multipass shell sonic-builder`
- From here, you have a ready and clean build environment.

Docker sonic VS build scripts are made for you in home dir, one to build arm & one x86. 
Note that you may want to edit these to checkout a different version of sonic, since
sometimes builds just don't work otherwise. By default, the scripts use the master branch.
To change the branch, add e.g. `git checkout 202106` **before** the sed lines because
they modify `rules/config`.
- `./build-vs-arm-docker.sh`
- `./build-vs-docker.sh`

Now pray to the Gods above, and perhaps you will end up with a working docker image :).

Notes on using the docker images:
~/sonic-buildimage/platform/vs/README.vsdocker.md 
