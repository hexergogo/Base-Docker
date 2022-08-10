# FROM ubuntu:20.04

# RUN sed -i s@/archive.ubuntu.com/@/mirrors.tuna.tsinghua.edu.cn/@g /etc/apt/sources.list && \
#   apt update && apt install -y vim wget curl &&  \
#   mkdir /root/.pip && \
#   echo "[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple\n[install]\ntrusted-host=pypi.tuna.tsinghua.edu.cn" > /root/.pip/pip.conf

# COPY gotty /usr/bin/gotty

# RUN chmod 777 /usr/bin/gotty

# EXPOSE 8080

# ENTRYPOINT ["/usr/bin/gotty"]
FROM hexu/intelliw-parallel:1.0

ARG BUILD="/build"

COPY distributed_pytorch /home/work/distributed_pytorch

RUN mkdir ${BUILD} && cd ${BUILD} && \
    wget http://10.167.3.4:33483/pypi/torch-1.11.0+cu102-cp38-cp38-linux_x86_64.whl        && \
    wget http://10.167.3.4:33483/pypi/torchaudio-0.11.0+cu102-cp38-cp38-linux_x86_64.whl  && \
    wget http://10.167.3.4:33483/pypi/torchvision-0.12.0+cu102-cp38-cp38-linux_x86_64.whl  && \
    wget http://10.167.3.4:33483/pypi/torchtext-0.12.0-cp38-cp38-linux_x86_64.whl  && \
    wget http://10.167.3.4:33483/distributed_demo/en_core_web_sm-3.3.0-py3-none-any.whl  && \
    wget http://10.167.3.4:33483/distributed_demo/zh_core_web_sm-3.3.0-py3-none-any.whl  && \
    pip install \
        torch-1.11.0+cu102-cp38-cp38-linux_x86_64.whl \
        torchaudio-0.11.0+cu102-cp38-cp38-linux_x86_64.whl \
        torchvision-0.12.0+cu102-cp38-cp38-linux_x86_64.whl \
        torchtext-0.12.0-cp38-cp38-linux_x86_64.whl \
        en_core_web_sm-3.3.0-py3-none-any.whl \
        zh_core_web_sm-3.3.0-py3-none-any.whl  && \
    pip install -r  /home/work/distributed_pytorch/requirements.txt && \
    rm -rf ${BUILD} /root/.pip/cache

