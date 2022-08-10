FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04

# declare environment variables
ENV WORK_DIR                     /bert
ENV PIP_FILE                     pip.conf
ENV WORK_DIR_MOUNT               mount
ENV APP_MODEL                    chinese_L-12_H-768_A-12.tar.gz
ENV START_SHELL                  wrapper_script.sh

## common system update
RUN \
    apt-get update && \
    apt-get check  && \
    apt-get -y autoremove    && \
    apt-get -y dist-upgrade  && \
    apt-get -y autoclean

# ========= install deadsnakes for python =========
RUN \
    apt-get -y install software-properties-common
RUN \
    add-apt-repository ppa:deadsnakes/ppa
RUN \
    apt-get update

RUN \
    apt-get -y install python3.6-venv python3.6-dev python3-pip curl virtualenv

RUN \
    mkdir -p $WORK_DIR

# Define mountable directories.
VOLUME $WORK_DIR/$WORK_DIR_MOUNT

# ========= python3.6 =========
# install pip config
# RUN mkdir -p /root/.pip
# add package
# ADD $PIP_FILE /root/.pip/
# install python package
RUN ln -s /usr/bin/python3.6 /usr/bin/python
# RUN ln -s /usr/bin/pip3 /usr/bin/pip
RUN curl https://bootstrap.pypa.io/get-pip.py|python

WORKDIR $WORK_DIR

# ========= bert =========
ADD $APP_MODEL $WORK_DIR/
RUN virtualenv -p python3.6 venv && \
    $WORK_DIR/venv/bin/pip install bert-serving-server==1.10.0 bert-serving-client==1.10.0 tensorflow-gpu==1.10

# ========= start shell =========
COPY $START_SHELL $WORK_DIR/

# export port
EXPOSE 5555
EXPOSE 5556

# start here
CMD chmod +x $WORK_DIR/$START_SHELL && $WORK_DIR/$START_SHELL

# DEBUG
#CMD $WORK_DIR/venv/bin/python -V && ls -la $WORK_DIR/venv/bin && \
#    $WORK_DIR/venv/bin/pip list                                                                                                                                                                                                                                                                                                                                                                1,1           All