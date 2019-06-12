FROM docker.io/ubuntu:18.04

# install dependencies including openslide
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/lib
ENV PATH="/home/cc/.local/red/bin:/home/cc/.local/bin:${PATH}"

RUN apt-get update \
&& apt-get install -y libjpeg-dev libtiff-dev libglib2.0-dev libcairo2-dev ibgdk-pixbuf2.0-dev libxml2-dev \
libsqlite3-dev valgrind zlib1g-dev libopenjp2-tools libopenjp2-7-dev curl python3-venv python3-dev \
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

# install connectors
RUN python3 -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==0.6 red-connector-ssh==0.8 red-connector-xnat==0.12

# install app
ENV PYTHONPATH=/home/cc/.local/lib/python3.6/site-packages:${PYTHONPATH}

RUN cd \
&& curl -LO https://github.com/deep-projects/camelyon-utils/releases/download/0.2/camelyon_utils-0.2-py3-none-any.whl \
&& pip3 install --user --upgrade camelyon_utils-0.2-py3-none-any.whl \
&& rm camelyon_utils-0.2-py3-none-any.whl
