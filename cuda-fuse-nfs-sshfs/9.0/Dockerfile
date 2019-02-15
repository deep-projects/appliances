FROM nvidia/cuda:9.0-cudnn7-runtime

ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/lib
ENV PATH ${PATH}:/root/.local/bin

RUN apt-get update \
&& apt-get install -y curl unzip make xsltproc fuse libfuse-dev libtool m4 automake openssh-client cmake pkg-config udev ninja-build libglib2.0-dev python3-pip \
&& pip3 install --user meson \
&& cd \
&& curl -LO https://github.com/sahlberg/fuse-nfs/archive/91c69c52970ae7c539262d9d38976da5505f2a1f.zip \
&& curl -LO https://github.com/sahlberg/libnfs/archive/libnfs-3.0.0.zip \
&& curl -OL https://github.com/libfuse/sshfs/releases/download/sshfs-2.10/sshfs-2.10.tar.gz \
&& unzip 91c69c52970ae7c539262d9d38976da5505f2a1f.zip \
&& unzip libnfs-3.0.0.zip \
&& tar -xvzf sshfs-2.10.tar.gz \
&& cd libnfs-libnfs-3.0.0 \
&& libtoolize \
&& aclocal \
&& autoheader \
&& autoconf \
&& automake --add-missing \
&& ./configure \
&& make \
&& make install \
&& cd ../fuse-nfs-91c69c52970ae7c539262d9d38976da5505f2a1f \
&& ./setup.sh \
&& ./configure \
&& make \
&& make install \
&& cd .. \
&& mkdir sshfs-2.10/build \
&& cd sshfs-2.10/build \
&& meson .. \
&& ninja install \
&& cd ../.. \
&& rm -r *libnfs-3.0.0* \
&& rm -r *91c69c52970ae7c539262d9d38976da5505f2a1f* \
&& rm -r sshfs-2.10*
