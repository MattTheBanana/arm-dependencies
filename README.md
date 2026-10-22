# arm-dependencies

[![Deploy Docker Image](https://github.com/automatic-ripping-machine/arm-dependencies/actions/workflows/deploy-docker.yml/badge.svg)](https://github.com/automatic-ripping-machine/arm-dependencies/actions/workflows/deploy-docker.yml)
[![Docker](https://img.shields.io/docker/pulls/automaticrippingmachine/arm-dependencies.svg)](https://hub.docker.com/r/automaticrippingmachine/arm-dependencies)

[![GitHub license](https://img.shields.io/github/license/automatic-ripping-machine/arm-dependencies)](https://github.com/automatic-ripping-machine/arm-dependencies/blob/main/LICENSE)
[![GitHub forks](https://img.shields.io/github/forks/automatic-ripping-machine/arm-dependencies)](https://github.com/automatic-ripping-machine/arm-dependencies/network)
[![GitHub stars](https://img.shields.io/github/stars/automatic-ripping-machine/arm-dependencies)](https://github.com/automatic-ripping-machine/arm-dependencies/stargazers)
[![GitHub issues](https://img.shields.io/github/issues/automatic-ripping-machine/arm-dependencies)](https://github.com/automatic-ripping-machine/arm-dependencies/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/automatic-ripping-machine/arm-dependencies)](https://github.com/automatic-ripping-machine/arm-dependencies/pulls)

![PyPI - Python Version](https://img.shields.io/pypi/pyversions/django)

[![Discord](https://img.shields.io/discord/576479573886107699)](https://discord.gg/FUSrn8jUcR)

## Overview
This repo codifies the requirements for building and running Automatic Ripping Machine, and provides a docker container that has everything preinstalled. All you need to do is install the ARM source and set up files.

The `arm-dependencies`Docker image is rebuilt every night, so you should always get the most up-to-date versions of MakeMKV and Handbrake when you build ARM from this image.


## Usage
### Git Repo
To add this manually, run the following command:
```shell
git submodule add -b main https://github.com/automatic-ripping-machine/arm-dependencies arm-dependencies
git submodule update --init --recursive
git config -f .gitmodules submodule.arm-dependencies.update rebase
git submodule update --remote
```

In your fork's `requirements.txt`, replace everything with
```text
-r arm-dependencies/requirements.txt
```

### Docker Container
To base your docker container on `arm-dependencies`, add this to the top of your `Dockerfile`:
```dockerfile

FROM automaticrippingmachine/arm-dependencies AS base
```


## TrueNAS / custom dependency image

This fork publishes the custom dependency base image to GHCR:

- Pinned base image: `ghcr.io/mattthebanana/arm-dependencies-custom:2.0.0`
- Moving tag: `ghcr.io/mattthebanana/arm-dependencies-custom:latest`

The TrueNAS ARM image uses the pinned `2.0.0` tag. The custom workflow rebuilds and publishes both tags from `main`. For unauthenticated pulls from TrueNAS, make the GHCR package public; otherwise configure image-pull credentials in TrueNAS.
