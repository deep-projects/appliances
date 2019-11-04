FROM docker.io/ubuntu:18.04

# install dependencies including openslide
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/lib

RUN apt-get update \
&& apt-get install -y libjpeg-dev libtiff-dev libglib2.0-dev libcairo2-dev ibgdk-pixbuf2.0-dev libxml2-dev \
libsqlite3-dev valgrind zlib1g-dev libopenjp2-tools libopenjp2-7-dev curl python3-venv python3-dev python3-pip \
&& useradd -ms /bin/bash cc \
&& cd \
&& curl -LO https://github.com/openslide/openslide/releases/download/v3.4.1/openslide-3.4.1.tar.gz \
&& tar -xvzf openslide-3.4.1.tar.gz \
&& cd openslide-3.4.1 \
&& ./configure \
&& make \
&& make install \
&& cd .. \
&& rm -r openslide-3.4.1*

# switch user
USER cc

ENV PATH=/home/cc/.local/bin:${PATH}

RUN mkdir -p /home/cc/.local/bin

# install connectors
RUN python3 -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==1.0 red-connector-ssh==1.1 red-connector-xnat==1.0 red-connector-ftp==0.3.0 \
&& ln -s /home/cc/.local/red/bin/red-connector-* /home/cc/.local/bin

# install app
ENV PYTHONPATH=/home/cc/.local/lib/python3.6/site-packages:${PYTHONPATH}

RUN cd \
&& curl -fLO https://github.com/deep-projects/camelyon-utils/releases/download/0.5/camelyon_utils-0.5-py3-none-any.whl \
&& pip3 install --user --upgrade camelyon_utils-0.5-py3-none-any.whl \
&& rm camelyon_utils-0.5-py3-none-any.whl
