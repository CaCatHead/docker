FROM ubuntu:22.04

ENV GCC_VERSION="12" \
    LLVM_VERSION="14" \
    OPENJDK_VERSION="17"

RUN apt-get update \
  && apt-get dist-upgrade -y \
  && apt-get install -y gnupg ca-certificates curl wget unzip zip locales \
  && locale-gen en_US.UTF-8 \
  && export DEBIAN_FRONTEND=noninteractive \
  && export LC_ALL=en_US.UTF-8 \
  && export TZ=Asia/Shanghai

RUN export UBUNTU_CODENAME="$(. /etc/os-release && echo "$UBUNTU_CODENAME")" \
  && export UBUNTU_VERSION="$(. /etc/os-release && echo "$VERSION_ID")" \
  # Key: LLVM repo
  && wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - \
  # Key: Python repo
  && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys BA6932366A755776 \
  # Key: Go repo
  && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys F6BC817356A3D45E \
  && echo "deb http://apt.llvm.org/$UBUNTU_CODENAME/ llvm-toolchain-$UBUNTU_CODENAME-$LLVM_VERSION main" > /etc/apt/sources.list.d/llvm.list \
  && echo "deb http://ppa.launchpad.net/deadsnakes/ppa/ubuntu $UBUNTU_CODENAME main" > /etc/apt/sources.list.d/python.list \
  && echo "deb http://ppa.launchpad.net/longsleep/golang-backports/ubuntu $UBUNTU_CODENAME main" >  /etc/apt/sources.list.d/go.list \
  && apt-get update \
  && apt-get install -y g++-$GCC_VERSION-multilib \
                        gcc-$GCC_VERSION-multilib \
                        clang-$LLVM_VERSION \
                        libc++-$LLVM_VERSION-dev \
                        libc++abi-$LLVM_VERSION-dev \
                        openjdk-$OPENJDK_VERSION-jdk \
                        python2.7 \
                        python3.9 \
                        python3.10 \
                        golang-go \
  && ln -s /usr/bin/g++-$GCC_VERSION /usr/local/bin/g++ \
  && ln -s /usr/bin/gcc-$GCC_VERSION /usr/local/bin/gcc \
  && ln -s /usr/bin/clang-$LLVM_VERSION /usr/local/bin/clang \
  && ln -s /usr/bin/clang++-$LLVM_VERSION /usr/local/bin/clang++

ADD ./testlib/testlib.h /usr/include/

RUN apt-get clean \
  && apt-get autoclean \
  && apt-get autoremove \
  && gcc --version \
  && g++ --version \
  && clang --version \
  && clang++ --version \
  && java -version
