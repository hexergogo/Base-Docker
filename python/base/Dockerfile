FROM ubuntu:20.04

ENV CONDA_DIR="/opt/conda"
ENV PATH="$CONDA_DIR/bin:$PATH"

COPY sources.list /etc/apt/

RUN  apt update && apt upgrade -y && apt install -y vim curl wget  &&  \
      mkdir /root/.pip && \
      echo "[global]\nindex-url = http://mirrors.aliyun.com/pypi/simple\n[install]\ntrusted-host=mirrors.aliyun.com" > /root/.pip/pip.conf

# Install conda
# python3.6 CONDA_VERSION="Miniconda3-4.3.31-Linux-x86_64.sh" CONDA_MD5_CHECKSUM="7fe70b214bee1143e3e3f0467b71453c"
# python3.7 CONDA_VERSION="Miniconda3-py37_4.11.0-Linux-x86_64.sh" CONDA_MD5_CHECKSUM="7675bd23411179956bcc4692f16ef27d"
# python3.8 CONDA_VERSION="Miniconda3-py38_4.11.0-Linux-x86_64.sh" CONDA_MD5_CHECKSUM="252d3b0c863333639f99fbc465ee1d61"
# python3.9 CONDA_VERSION="Miniconda3-py39_4.11.0-Linux-x86_64.sh" CONDA_MD5_CHECKSUM="4e2f31e0b2598634c80daa12e4981647"

RUN CONDA_VERSION="Miniconda3-py39_4.11.0-Linux-x86_64.sh" && \
    CONDA_MD5_CHECKSUM="4e2f31e0b2598634c80daa12e4981647" && \
    mkdir -p "$CONDA_DIR" && \
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


RUN pip config set extra-index-url http://mirrors.aliyun.com/pypi/simple/ && \
    pip config set install.trusted-host mirrors.aliyun.com
