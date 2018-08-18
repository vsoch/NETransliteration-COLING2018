FROM tensorflow/tensorflow:1.4.1-py3

# docker build -t vanessa/netransliteration-coling2018-cpu -f docker/Dockerfile .
# docker run -it --name ntc-cpu vanessa/netransliteration-coling2018-cpu bash

LABEL maintainer vsochat@stanford.edu
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y install locales && \
    locale-gen en_US.UTF-8 && \
    apt-get install -y git wget python3-dev python3-pip python3-tk && \
    apt-get clean && \
    apt-get install -y libcupti-dev && \
    python3 -m pip install tensorflow==1.4.1 tensor2tensor==1.3.2

RUN mkdir -p /code/models
ADD . /code/
