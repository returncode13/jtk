FROM ubuntu:22.04

ARG UNAME=dev
ARG UID=1000
ARG GID=1000
RUN groupadd -g $GID -o $UNAME
RUN useradd -m -u $UID -g $GID -o -s /bin/bash $UNAME
USER $UNAME
ENV DEBIAN_FRONTEND noninteractive
WORKDIR /home/${UNAME}
USER root
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    python3-pip \
    libasound2 \
    libc6-i386 \
    libc6-x32 \
    libfreetype6 \
    libx11-6 \
    libxext6 \
    libxi6 \
    libxrender1 \
    libxtst6 \
    unzip



#Install JDK-17. JRE is included 
COPY deps/jdk-17_linux-x64_bin.deb  .
RUN dpkg -i jdk-17_linux-x64_bin.deb 


#Install gradle .
COPY deps/gradle-7.6-bin.zip .
RUN mkdir /opt/gradle && unzip -d /opt/gradle gradle-7.6-bin.zip

#Install git 
RUN apt-get install -y git 



USER $UNAME
RUN mkdir app
RUN git clone https://github.com/xinwucwp/sos.git

RUN echo "export PATH=$PATH:/opt/gradle/gradle-7.6/bin:/usr/lib/jvm/jdk-17/bin/" >> /home/${UNAME}/.bashrc
# RUN echo "export PATH=$PATH:/usr/lib/jvm/jdk-17/bin/" >> /home/${UNAME}/.bashrc

# # Install package dependencies
# RUN apt-get update -y && \
#     apt-get install -y --no-install-recommends \
#         python3-pip \
        
#build using docker build --build-arg UID=$(id -u) --build-arg GID=$(id -g) -t image_name:tag .
