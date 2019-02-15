FROM nvidia/cuda:9.0-cudnn7-runtime

ENV PATH ${PATH}:/root/.local/bin

RUN apt-get update \
&& apt-get install -y curl fuse make gcc openssh-client ninja-build libgumbo-dev \
libfuse-dev libssl-dev libcurl4-openssl-dev python3-pip pkg-config libglib2.0-dev \
&& pip3 install --user meson \
&& cd \
&& curl -LO https://github.com/fangfufu/httpdirfs/archive/v1.0.1.tar.gz \
&& curl -LO https://github.com/libfuse/sshfs/releases/download/sshfs-2.10/sshfs-2.10.tar.gz \
&& tar -xvzf v1.0.1.tar.gz \
&& tar -xvzf sshfs-2.10.tar.gz \
&& cd httpdirfs-1.0.1 \
&& sed -i 's/$(CC) $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -c -o $@ $</$(CC) -o $@ $< $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -c/' Makefile \
&& sed -i 's/$(CC) $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -o $@ $^/$(CC) -o $@ $^ $(CPPFLAGS) $(CFLAGS) $(LDFLAGS)/' Makefile \
&& make \
&& make install \
&& cd .. \
&& mkdir sshfs-2.10/build \
&& cd sshfs-2.10/build \
&& meson .. \
&& ninja install \
&& cd ../.. \
&& rm -r *1.0.1* \
&& rm -r sshfs-2.10*
