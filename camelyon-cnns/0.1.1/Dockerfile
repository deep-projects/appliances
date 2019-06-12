FROM docker.io/somnonetz/tensorflow:1.13.1-gpu-py3.7

USER root

RUN apt-get update \
&& apt-get install -y sshfs
#python3-pip python3-venv libffi-dev libssl-dev python3-dev

# switch user
USER cc

ENV PATH="/home/cc/.local/red/bin:/home/cc/.local/bin:${PATH}"

# install connectors
RUN python -m venv /home/cc/.local/red \
&& . /home/cc/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==0.6 red-connector-ssh==0.8 red-connector-xnat==0.12

# install app
RUN cd \
&& curl -LO https://github.com/deep-projects/camelyon-cnns/releases/download/0.1/camelyon_cnns-0.1-py3-none-any.whl \
&& pip install --user --upgrade camelyon_cnns-0.1-py3-none-any.whl \
&& rm camelyon_cnns-0.1-py3-none-any.whl

ENV PYTHONPATH="/home/cc/.local/lib/python3.5/site-packages:/usr/local/lib/python3.5/dist-packages:${PYTHONPATH}"
