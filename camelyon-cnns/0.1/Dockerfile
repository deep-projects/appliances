FROM deepprojects/tensorflow-sshfs:1.12.0-3.5.1

RUN apt-get update \
&& apt-get install -y git python3-pip python3-venv libffi-dev libssl-dev python3-dev \
&& useradd -ms /bin/bash cc

# switch user
USER cc

ENV PATH="/home/cc/.local/red/bin:/home/cc/.local/bin:${PATH}"

# install connectors
RUN python3 -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==0.3 red-connector-ssh==0.5 red-connector-xnat==0.9 red-connector-sshfs==0.2

# install app
RUN cd \
&& curl -LO https://github.com/deep-projects/camelyon-cnns/releases/download/0.1/camelyon_cnns-0.1-py3-none-any.whl \
&& pip3 install --user --upgrade camelyon_cnns-0.1-py3-none-any.whl \
&& rm camelyon_cnns-0.1-py3-none-any.whl

ENV PYTHONPATH="/home/cc/.local/lib/python3.5/site-packages:/usr/local/lib/python3.5/dist-packages:${PYTHONPATH}"
