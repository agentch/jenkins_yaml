FROM jenkinsci/jnlp-slave
LABEL maintainer changbin<changbin@guiji.ai>

USER root
# timezone
RUN apt-get update && \
 apt-get install -y tzdata && \
 ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
 echo "Asia/Shanghai" > /etc/timezone

# install maven
RUN apt-get install curl tar bash
ARG MAVEN_VERSION=3.3.9
ARG USER_HOME_DIR="/home/jenkins"
RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
 && curl -fsSL https://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
 | tar -xzC /usr/share/maven --strip-components=1 \
 && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

# Install Docker client
ENV DOCKER_BUCKET download.docker.com
ENV DOCKER_VERSION 19.03.8
RUN set -x \
 && curl -fSL "https://${DOCKER_BUCKET}/linux/static/stable/x86_64/docker-$DOCKER_VERSION.tgz" -o docker.tgz \
 && tar -xzvf docker.tgz \
 && mv docker/* /usr/local/bin/ \
 && rmdir docker \
 && rm docker.tgz \
 && docker -v

#kubectl
COPY kubectl ./kubectl
RUN chmod +x kubectl \
 && mv ./kubectl /usr/local/bin/kubectl
 
 #Switch user to jenkins
 USER jenkins
