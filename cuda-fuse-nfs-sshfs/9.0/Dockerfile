FROM nvidia/cuda:9.0-base

RUN apt-get update \
&& apt-get install -y curl unzip make xsltproc libfuse-dev libtool m4 automake libnfs-dev sshfs \
&& cd \
&& curl -LO https://github.com/sahlberg/fuse-nfs/archive/91c69c52970ae7c539262d9d38976da5505f2a1f.zip \
&& unzip 91c69c52970ae7c539262d9d38976da5505f2a1f.zip \
&& cd fuse-nfs-91c69c52970ae7c539262d9d38976da5505f2a1f \
&& ./setup.sh \
&& ./configure \
&& make \
&& make install \
&& cd \
&& rm -r *91c69c52970ae7c539262d9d38976da5505f2a1f*
