FROM python:3.8-alpine3.12
 
ENV PYTHONUNBUFFERED 1
 
#换国内源，必须都加上，否则openjdk不能通过apk add下载
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories
 
RUN apk update && apk add bash
 
# 添加glibc依赖-用官方jdk安装时的必要依赖，此处我不确定openjdk是不是也需要
RUN apk --no-cache add ca-certificates 
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
#以下命令github连接有时可能下载失败（注释行），可以先手动下载后，放到dokerfile同级的envimportfile文件夹中，用copy命令拷贝到容器。
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk
RUN apk add glibc-2.29-r0.apk
 
# install openjdk8
RUN apk add openjdk8
ENV JAVA_HOME=/usr/lib/jvm/default-jvm
ENV CLASSPATH=$JAVA_HOME/bin
ENV PATH=.:$JAVA_HOME/bin:$PATH
 
# download spark
RUN wget http://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-3.2.2/spark-3.2.2-bin-hadoop3.2.tgz
RUN tar -zvxf spark-3.2.2-bin-hadoop3.2.tgz
 
# config spark
# RUN vi ~/.bash_profile
ENV SPARK_HOME=/spark-3.2.2-bin-hadoop3.2
ENV PATH=$SPARK_HOME/bin:$PATH
ENV PYTHONPATH=$SPARK_HOME/python/:$PYTHONPATH 
 
WORKDIR /app
 
RUN pip install --upgrade pip -i https://pypi.tuna.tsinghua.edu.cn/simple/
RUN pip install pyspark -i https://pypi.tuna.tsinghua.edu.cn/simple/
RUN pip install py4j -i https://pypi.tuna.tsinghua.edu.cn/simple/
 
CMD /bin/sh