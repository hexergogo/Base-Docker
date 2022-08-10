FROM hexergogo/python:3.8
 
RUN apt update && apt install -y ssh

# install pyspark
RUN pip install pyspark -i https://pypi.tuna.tsinghua.edu.cn/simple/
 
# install openjdk8
ARG jdkPath=/usr/lib/jvm/jdk
ARG jdkPackage=jdk-8u202-linux-x64
RUN mkdir /usr/lib/jvm && cd /usr/lib/jvm && wget https://repo.huaweicloud.com/java/jdk/8u202-b08/${jdkPackage}.tar.gz
RUN cd /usr/lib/jvm && tar -zvxf ${jdkPackage}.tar.gz  && mv jdk1.8.0_202 ${jdkPath}  &&  rm -rf ${jdkPackage}.tar.gz
ENV JAVA_HOME=${jdkPath}
ENV CLASSPATH=$JAVA_HOME/bin
ENV PATH=.:$JAVA_HOME/bin:$PATH
 

WORKDIR /home/work

# download 
ARG hadoopPackage=hadoop-3.3.3
ARG sparkPackage=spark-3.3.0-bin-hadoop3
RUN wget https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/core/hadoop-3.3.3/${hadoopPackage}.tar.gz
RUN wget https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-3.3.0/${sparkPackage}.tgz

# install spark
ENV SPARK_HOME=/home/work/spark-3.3.0
ENV PATH=$SPARK_HOME/bin:$PATH
RUN tar -zvxf ${sparkPackage}.tgz  && mv ${sparkPackage} ${SPARK_HOME} && rm -rf ${sparkPackage}.tgz

# install hadoop
ENV HADOOP_HOME=/home/work/hadoop-3.3.3
ENV PATH=$HADOOP_HOME/bin:$PATH
ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
RUN tar -zvxf ${hadoopPackage}.tar.gz && rm -rf ${hadoopPackage}.tar.gz

# claen
RUN apt clean && rm -rf ~/.cache 

# ssh
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
    chmod 0600 ~/.ssh/authorized_keys && \
    echo "service ssh start"  >> ~/.bashrc


# master-web-port  worker-server-port  task-web-port  spark-history-port
EXPOSE 8080 7077 4040 18080