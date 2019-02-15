FROM docker.io/deepprojects/cuda-sshfs:9.0-3.5.1

RUN apt-get update \
&& apt-get install -y git python3-venv libffi-dev libssl-dev python3-dev \
&& useradd -ms /bin/bash cc

# switch user
USER cc

ENV PATH="/home/cc/.local/red/bin:/home/cc/.local/bin:/home/cc/.poetry/bin:${PATH}"

# install connectors
RUN python3 -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==0.3 red-connector-ssh==0.5 red-connector-xnat==0.9 red-connector-sshfs==0.2

# install app
RUN cd \
&& mkdir -p /home/cc/.local/bin \
&& ln -s $(which python3) /home/cc/.local/bin \
&& curl -sSL https://raw.githubusercontent.com/sdispater/poetry/master/get-poetry.py | python \
&& pip3 install --user --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.12.0-cp35-cp35m-linux_x86_64.whl

RUN cd \
&& git clone https://github.com/deep-projects/camelyon-cnns.git \
&& cd camelyon-cnns \
&& . /home/cc/.poetry/env \
&& poetry build --format=wheel \
&& pip3 install --user --upgrade dist/*.whl \
&& rm -rf camelyon-cnns

ENV PYTHONPATH="/home/cc/.local/lib/python3.5/site-packages/:${PYTHONPATH}"