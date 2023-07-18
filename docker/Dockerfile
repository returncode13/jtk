FROM ubuntu:22.04


ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    python2-minimal \
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


WORKDIR /app

#Install JDK-17. JRE is included 
COPY deps/jdk-17_linux-x64_bin.deb  .
RUN dpkg -i jdk-17_linux-x64_bin.deb 


#Install gradle .
COPY deps/gradle-7.6-bin.zip .
RUN mkdir /opt/gradle && unzip -d /opt/gradle gradle-7.6-bin.zip

# #Copy jy script
# COPY scripts/jy .  
#Dont copy jy script . The script should be custom to the app. so must be present in the app folder

#Install git 
RUN apt-get install -y git 



ENV PATH="$PATH:/opt/gradle/gradle-7.6/bin:/usr/lib/jvm/jdk-17/bin/:/app/sos/bin"
ENV JAVA_LIBRARY_PATH="/usr/lib/jvm/jdk-17/lib"
#Clone jtk
RUN git clone https://github.com/returncode13/rez-jtk.git /app/jtk
#Build jtk
RUN cd /app/jtk && sh gradlew

