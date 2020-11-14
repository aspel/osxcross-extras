# base image, not the final image
FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get full-upgrade -y
RUN apt-get install -y build-essential wget python2.7 python3 \
 python3-pip python3-distutils cmake git p7zip-full libarchive-tools curl \
 cpio xz-utils patch pixz sudo libxml2-dev libssl-dev \
 zlib1g-dev liblzma-dev libbz2-dev \
 software-properties-common
RUN wget -O llvm-snapshot.gpg.key https://apt.llvm.org/llvm-snapshot.gpg.key|apt-key add llvm-snapshot.gpg.key
RUN apt-add-repository 'deb http://apt.llvm.org/focal/ llvm-toolchain-focal-11 main'
RUN apt-get update
RUN apt-get install -y clang-11 llvm-11
COPY * /tmp/
RUN /tmp/ci.sh

# second stage
FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get full-upgrade -y
RUN apt-get install -y build-essential cmake wget git p7zip-full ccache ninja-build software-properties-common
RUN wget -O llvm-snapshot.gpg.key https://apt.llvm.org/llvm-snapshot.gpg.key|apt-key add llvm-snapshot.gpg.key
RUN apt-add-repository 'deb http://apt.llvm.org/focal/ llvm-toolchain-focal-11 main'
RUN apt-get update
RUN apt-get install -y clang-11 llvm-11
COPY --from=0 /opt/osxcross /opt/osxcross
ENV PATH="${PATH}:/opt/osxcross/bin/"
