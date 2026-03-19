FROM ubuntu:22.04

WORKDIR /tmp/project

ENV DEBIAN_FRONTEND=noninteractive

# Make Dependecies for AWX Build from Dockerfile.sdist:
RUN apt update && \
    apt install -y python3-pip ansible make virtualenv

RUN virtualenv .venvpy3

RUN pip install ansible-builder==3.1.0

ADD playbook-prepare-build-files.yml /tmp/project/

RUN ansible-playbook playbook-prepare-build-files.yml

# Files in config folder specify the configuration of the final awx-ee image
ADD config/* /tmp/project/

CMD ansible-builder build  -v 3 --tag=awx_ee_slm_devel:latest --container-runtime=docker