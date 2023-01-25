FROM ubuntu:22.04

ENV GCC_VERSION="12" \
    LLVM_VERSION="14" \
    OPENJDK_VERSION="17"

RUN apt-get update \
  && apt-get install -y g++-$GCC_VERSION-multilib \
                        gcc-$GCC_VERSION-multilib \
                        openjdk-$OPENJDK_VERSION-jdk

RUN ln -s /usr/bin/g++-$GCC_VERSION /usr/local/bin/g++ \
  && ln -s /usr/bin/gcc-$GCC_VERSION /usr/local/bin/gcc

RUN apt-get clean && apt-get autoclean && apt-get autoremove

RUN gcc --version \
  && g++ --version \
  && java -version
