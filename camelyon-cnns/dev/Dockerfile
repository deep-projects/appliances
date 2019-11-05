FROM docker.io/nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04

RUN apt-get update \
&& apt-get install -y git python3-venv python3-pip sshfs curl \
&& useradd -ms /bin/bash cc

# switch user
USER cc

ENV PATH /home/cc/.local/bin:/home/cc/.poetry/bin:${PATH}

RUN mkdir -p /home/cc/.local/bin

# install connectors
RUN python3 -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==1.0 red-connector-ssh==1.2 red-connector-xnat==1.0 red-connector-ftp==1.0 \
&& ln -s /home/cc/.local/red/bin/red-connector-* /home/cc/.local/bin

# install poetry
RUN cd \
&& ln -s $(which python3) /home/cc/.local/bin/python \
&& curl -sSL https://raw.githubusercontent.com/sdispater/poetry/master/get-poetry.py | python

# install app
RUN cd \
&& git clone https://github.com/deep-projects/camelyon-cnns.git \
&& cd camelyon-cnns \
&& poetry build --format=wheel \
&& pip3 install --user --upgrade tensorflow-gpu==1.13.1 dist/*.whl \
&& rm -rf camelyon-cnns

#ENV PYTHONPATH="/home/cc/.local/lib/python3.5/site-packages:/usr/local/lib/python3.5/dist-packages:${PYTHONPATH}"
