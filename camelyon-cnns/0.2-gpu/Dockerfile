FROM docker.io/nvidia/cuda:10.0-cudnn7-runtime-ubuntu18.04

RUN apt-get update \
&& apt-get install -y python3-venv python3-pip sshfs curl \
&& useradd -ms /bin/bash cc

# switch user
USER cc

ENV PATH /home/cc/.local/bin:${PATH}

RUN mkdir -p /home/cc/.local/bin

# install connectors
RUN python3 -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==1.0 red-connector-ssh==1.2 red-connector-xnat==1.0 red-connector-ftp==1.0 \
&& ln -s /home/cc/.local/red/bin/red-connector-* /home/cc/.local/bin

# install app
RUN cd \
&& curl -fLO https://github.com/deep-projects/camelyon-cnns/releases/download/0.2/camelyon_cnns-0.2-py3-none-any.whl \
&& pip3 install --user --upgrade tensorflow-gpu==1.13.1 camelyon_cnns-0.2-py3-none-any.whl \
&& rm camelyon_cnns-0.2-py3-none-any.whl
