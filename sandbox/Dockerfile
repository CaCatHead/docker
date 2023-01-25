FROM ubuntu:22.04

RUN apt-get update \
  && apt-get dist-upgrade -y \
  && apt-get install -y gnupg ca-certificates curl wget unzip zip locales software-properties-common \
  && rm -rf /var/lib/apt/lists/* \
  && locale-gen en_US.UTF-8

ENV DEBIAN_FRONTEND=noninteractive \
    LC_ALL=en_US.UTF-8 \
    TZ=Asia/Shanghai \
    GCC_VERSION="12" \
    LLVM_VERSION="14" \
    OPENJDK_VERSION="17" \
    NODE_VERSION="18"

RUN export UBUNTU_CODENAME="$(. /etc/os-release && echo "$UBUNTU_CODENAME")" \
  && export UBUNTU_VERSION="$(. /etc/os-release && echo "$VERSION_ID")" \
  && wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - \
  && echo "deb http://apt.llvm.org/$UBUNTU_CODENAME/ llvm-toolchain-$UBUNTU_CODENAME-$LLVM_VERSION main" > /etc/apt/sources.list.d/llvm.list \
  && add-apt-repository ppa:deadsnakes/ppa \
  && add-apt-repository ppa:longsleep/golang-backports \
  && curl -sL https://deb.nodesource.com/setup_$NODE_VERSION.x  | bash - \
  && apt-get update \
  && apt-get install -y --no-install-recommends \
      g++-$GCC_VERSION-multilib \
      gcc-$GCC_VERSION-multilib \
      clang-$LLVM_VERSION \
      libc++-$LLVM_VERSION-dev \
      libc++abi-$LLVM_VERSION-dev \
      openjdk-$OPENJDK_VERSION-jdk \
      python2.7 \
      python3.10 \
      golang-go \
      nodejs \
  && ln -s /usr/bin/g++-$GCC_VERSION /usr/local/bin/g++ \
  && ln -s /usr/bin/gcc-$GCC_VERSION /usr/local/bin/gcc \
  && ln -s /usr/bin/clang-$LLVM_VERSION /usr/local/bin/clang \
  && ln -s /usr/bin/clang++-$LLVM_VERSION /usr/local/bin/clang++ \
  && apt-get clean \
  && apt-get autoclean \
  && apt-get autoremove \
  && rm -rf /var/lib/apt/lists/*

ADD ./testlib/testlib.h /usr/include/

RUN gcc --version \
  && g++ --version \
  && clang --version \
  && clang++ --version \
  && java -version \
  && go version \
  && node --version
