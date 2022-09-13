FROM ubuntu:20.04

RUN sed -i s@/archive.ubuntu.com/@/mirrors.tuna.tsinghua.edu.cn/@g /etc/apt/sources.list && \
  apt update && apt install -y vim wget curl &&  \
  mkdir /root/.pip && \
  echo "[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple\n[install]\ntrusted-host=pypi.tuna.tsinghua.edu.cn" > /root/.pip/pip.conf

COPY gotty /usr/bin/gotty

RUN chmod 777 /usr/bin/gotty

EXPOSE 8080

ENTRYPOINT ["/usr/bin/gotty"]


