# test-host-generation
Scripts for the generation of test docker hosts

# Requirements

Requires [Packer](http://packer.io/) from Hashicorp and [Virtualbox](https://www.virtualbox.org/) from Oracle.

# How to build

This repository contians several base machines that come with a single httpd container running. 
You can customise the packer.json files to install more containers etc. by expanding on the "provisioners" section. 
To perform the build cd into a subdirectory and invoke the command:

    $ packer build packer.json

# Simulate a hard shutdown 

If you want to simulate a power-off (hard shutdown), e. g. to analyse the remains of running containers, you can add the following lines to the packer file, to the section of the virtualbox-iso builder.

    "shutdown_command": "sudo poweroff --force --force --no-sync",

# Common issues

## SSH Authentication failures during build

    Build 'virtualbox-iso' errored: ssh: handshake failed: ssh: unable to authenticate,

SSH Authentication failures during the build happen mostly when packer connects to sshd before the system is fully installed and rebooted. To avoid this issue, shut down and don't start sshd during the setup process.
