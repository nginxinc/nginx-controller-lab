NGINX Controller Lab Guide
==========================

![Build Docs](https://github.com/nginxinc/nginx-controller-lab/workflows/Build%20Docs/badge.svg)

Introduction
------------

This repo contains the documentation sources for the NGINX Controller 3.x UDF lab.

Setup
-----

1. Download or `git clone` the nginx-controller-lab
2. Download and install Docker CE (https://docs.docker.com/engine/installation/)
3. Build the sample docs `./containthedocs-build.sh`. The first time you build
   a container (~1G in size) will be downloaded from Docker Hub.
4. Open the `docs/_build/html/index.html` file on you system in a web browser


Build Scripts
-------------

The repo includes build scripts for common operations:

- `containthedocs-bash.sh`: Run to container with a BASH prompt
- `containthedocs-build.sh`: Build HTML docs using `make -C docs html` to
  `docs/_build/html`
- `containthedocs-clean.sh`: Clean the build directory using
  `make -C docs clean`
- `containthedocs-cleanbuild.sh`: Clean the build directory and build HTML
  docs using `make -C docs clean html`
- `containthedocs-convert.sh`: Convert a Word `.docx` file to rST
- `containthedocs-pdf.sh`: Build PDF docs using `make -C docs latexpdf` to
  `docs/_build/latex`
