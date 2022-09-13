FROM hexergogo/python:3.8

# install openjdk8
ARG jdkPath=/usr/lib/jvm/jdk
ARG jdkPackage=jdk-8u202-linux-x64
RUN mkdir /usr/lib/jvm && cd /usr/lib/jvm && wget https://repo.huaweicloud.com/java/jdk/8u202-b08/${jdkPackage}.tar.gz
RUN cd /usr/lib/jvm && tar -zvxf ${jdkPackage}.tar.gz  && mv jdk1.8.0_202 ${jdkPath}  &&  rm -rf ${jdkPackage}.tar.gz
ENV JAVA_HOME=${jdkPath}
ENV CLASSPATH=$JAVA_HOME/bin
ENV PATH=.:$JAVA_HOME/bin:$PATH
 
# install pyspark
RUN pip install --upgrade pip && pip install JPype1

WORKDIR /home/work

# claen
RUN apt clean && rm -rf ~/.cache 