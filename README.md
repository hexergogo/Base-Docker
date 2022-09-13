# 🐳  Base Dockerfile  🐳

The usual base Dockerfile

## 🐳 Support

 ● gotty  
```
docker push hexergogo/gotty:2.0.0
```

 ● python  
 ```
 docker push hexergogo/python:3.6
 docker push hexergogo/python:3.7
 docker push hexergogo/python:3.8
 docker push hexergogo/python:3.9
 ```

 ● bert  
 ● pyspark  
 ```
docker push hexergogo/pyspark:3.3.0
 ``` 
 ● torch  

 ● pyjdk  
```
docker push hexergogo/pyjdk:py38-jdk8

JAVA_HOME=/usr/lib/jvm/jdk
CLASSPATH=$JAVA_HOME/bin

from jpype import *
if __name__ = "__main__":
    startJVM("/usr/lib/jvm/jdk/jre/lib/amd64/server/libjvm.so")
    java.lang.System.out.println("Hello World!")
    shutdownJVM()
``` 

## 🐳 Demo

 ● golang  
