FROM nvidia/cuda:10.2-cudnn8-devel-ubuntu18.04

ENV CONDA_DIR="/opt/conda"
ENV PATH="$CONDA_DIR/bin:$PATH"

# declare environment variables
ENV WORK_DIR                   /home/work

RUN sed -i "s@http://.*archive.ubuntu.com@http://repo.huaweicloud.com@g" /etc/apt/sources.list && \
    sed -i "s@http://.*security.ubuntu.com@http://repo.huaweicloud.com@g" /etc/apt/sources.list 

RUN mkdir /root/.pip && \
    echo "[global]\nindex-url = http://mirrors.aliyun.com/pypi/simple\n[install]\ntrusted-host=mirrors.aliyun.com" > /root/.pip/pip.conf 

RUN CONDA_VERSION="Miniconda3-py38_4.11.0-Linux-x86_64.sh" && \
    CONDA_MD5_CHECKSUM="252d3b0c863333639f99fbc465ee1d61" && \
    mkdir -p "$CONDA_DIR" && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    TZ=Asia/Shanghai \
    apt -y install  curl vim  wget   && \
    wget "http://repo.continuum.io/miniconda/${CONDA_VERSION}" -O miniconda.sh && \
    echo "$CONDA_MD5_CHECKSUM  miniconda.sh" | md5sum -c && \
    bash miniconda.sh -f -b -p "$CONDA_DIR" && \
    echo "export PATH=$CONDA_DIR/bin:\$PATH" > /etc/profile.d/conda.sh && \
    rm miniconda.sh && \
    conda update --all --yes && \
    conda config --set auto_update_conda False && \
    rm -r "$CONDA_DIR/pkgs/" && \
    apt-get clean && \
    mkdir -p "$CONDA_DIR/locks" && \
    chmod 777 "$CONDA_DIR/locks" && \
    python -m pip install  --upgrade pip

RUN apt-get install -y build-essential python3.8-dev && rm -rf /usr/lib/python3.6 /etc/python3.6 &&  apt-get clean

ARG BUILD="/build"

RUN mkdir ${BUILD} && cd ${BUILD} && \
    wget https://download.pytorch.org/whl/cu102/torch-1.11.0%2Bcu102-cp38-cp38-linux_x86_64.whl        && \
    wget https://download.pytorch.org/whl/cu102/torchaudio-0.11.0%2Bcu102-cp38-cp38-linux_x86_64.whl  && \
    wget https://download.pytorch.org/whl/cu102/torchvision-0.12.0%2Bcu102-cp38-cp38-linux_x86_64.whl  && \
    wget https://download.pytorch.org/whl/torchtext-0.12.0-cp38-cp38-linux_x86_64.whl  && \
    pip install \
        torch-1.11.0+cu102-cp38-cp38-linux_x86_64.whl \
        torchaudio-0.11.0+cu102-cp38-cp38-linux_x86_64.whl \
        torchvision-0.12.0+cu102-cp38-cp38-linux_x86_64.whl \
        torchtext-0.12.0-cp38-cp38-linux_x86_64.whl && \ 
    rm -rf ${BUILD} /root/.pip/cache