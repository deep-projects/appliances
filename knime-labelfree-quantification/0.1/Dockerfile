FROM docker.io/fbartusch/knime-labelfree-quantification:1.0

USER root

# prepare folders
RUN rm /tmp \
&& mkdir -p /tmp /output/tmp /output/knime_tmp/workflow \
&& cp -r /payload/workflow /output/knime_tmp \
&& chmod 777 /tmp \
&& chown -R knime:knime /input \
&& chown -R knime:knime /output \
&& rm /etc/apt/sources.list.d/webupd8team-ubuntu-java-bionic.list

# install dependencies for RED connectors
RUN apt-get update \
&& apt-get install -y python3-pip python3-venv curl git

USER knime

ENV PATH /home/knime/.local/bin:${PATH}
ENV KNIME_DIR /usr/local/knime/
ENV HOME_DIR /home/knime/
ENV TMP /output/tmp
ENV TMPDIR /output/tmp

# install RED connectors
RUN mkdir -p /home/knime/.local/bin \
&& python3 -m venv /home/knime/.local/red \
&& . /home/knime/.local/red/bin/activate \
&& pip install wheel \
&& pip install red-connector-http==0.6 red-connector-ssh==0.8 \
&& ln -s /home/knime/.local/red/bin/red-connector-* /home/knime/.local/bin

# install app
ADD --chown=knime:knime run-knime /home/knime/.local/bin/run-knime

ENTRYPOINT []
