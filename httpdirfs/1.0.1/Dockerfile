FROM docker.io/debian:buster-slim

RUN apt-get update \
&& apt-get install -y curl libgumbo-dev libfuse-dev libssl-dev libcurl4-openssl-dev fuse make gcc \
&& cd \
&& curl -LO https://github.com/fangfufu/httpdirfs/archive/v1.0.1.tar.gz \
&& tar -xvzf v1.0.1.tar.gz \
&& cd httpdirfs-1.0.1 \
&& make \
&& make install \
&& cd .. \
&& rm -r *1.0.1*
