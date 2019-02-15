FROM nvidia/cuda:9.0-cudnn7-runtime

ENV LD_LIBRARY_PATH ${LD_LIBRARY_PATH}:/usr/local/lib/x86_64-linux-gnu
ENV PATH ${PATH}:/root/.local/bin

RUN apt-get update \
&& apt-get install -y openssh-client curl cmake pkg-config udev ninja-build libglib2.0-dev xz-utils python3-pip \
&& pip3 install --user meson \
&& cd \
&& curl -OL https://github.com/libfuse/libfuse/releases/download/fuse-3.4.1/fuse-3.4.1.tar.xz \
&& curl -OL https://github.com/libfuse/sshfs/releases/download/sshfs-3.5.1/sshfs-3.5.1.tar.xz \
&& tar -xf fuse-3.4.1.tar.xz \
&& tar -xf sshfs-3.5.1.tar.xz \
&& mkdir fuse-3.4.1/build \
&& mkdir sshfs-3.5.1/build \
&& cd fuse-3.4.1/build \
&& meson .. \
&& ninja install \
&& cd ../../sshfs-3.5.1/build \
&& meson .. \
&& ninja install \
&& cd ../.. \
&& rm -r fuse-3.4.1* \
&& rm -r sshfs-3.5.1*
