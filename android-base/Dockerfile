FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN dpkg --add-architecture i386 && apt-get update -yqq && apt-get install -y \
  sudo \
  curl \
  wget \
  expect \
  git \
  libunwind8 \
  uuid-runtime \
  subversion \
  zip \
  unzip \
  openjdk-8-jdk \
  cmake \
  gcc \
  g++ \
  ninja-build \
  && apt-get clean

RUN mkdir /agent
COPY vsts-agent-linux-x64-2.140.2.tar.gz /agent/vsts-agent.tar.gz
WORKDIR "/agent"
RUN tar zxf vsts-agent.tar.gz
RUN chmod -R 777 /agent

RUN ./bin/installdependencies.sh

RUN update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
RUN update-alternatives --set javac /usr/lib/jvm/java-8-openjdk-amd64/bin/javac

RUN mkdir -p /opt/android-sdk && \
    chmod -R 777 /opt

RUN useradd -m agent
USER agent
RUN umask 777
WORKDIR /opt/android-sdk

RUN wget -q https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip && \
    unzip -q sdk-tools-linux-4333796.zip && \
    rm sdk-tools-linux-4333796.zip
ENV ANDROID_SDK /opt/android-sdk
ENV ANDROID_SDK_HOME /opt/android-sdk
ENV ANDROID_SDK_ROOT /opt/android-sdk
ENV ANDROID_HOME /opt/android-sdk
ENV AndroidSDK /opt/android-sdk

RUN yes | ${AndroidSDK}/tools/bin/sdkmanager --licenses

RUN mkdir -p ${ANDROID_SDK}/.android && \
    touch ${ANDROID_SDK}/.android/repositories.cfg

ENV GYP_GENERATORS=ninja
