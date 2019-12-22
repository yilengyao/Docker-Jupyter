FROM ubuntu:18.04
# Java 8 (Oracle) Dockerfile
# Base image: Ubuntu
# Installs: Java 8

# Install basic software support
RUN apt-get update && \
    apt-get install --yes software-properties-common

# Add the JDK 8 and accept licenses (mandatory)
RUN add-apt-repository ppa:webupd8team/java && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections

# Install Java 8
RUN apt-get update && \
    apt-get --yes --no-install-recommends install openjdk-11-jdk openjdk-11-jre

RUN apt-get update
RUN apt-get install -y python3-pip && \
    apt-get install -y curl unzip

# add requirements.txt, written this way to gracefully ignore a missing file
COPY . .
RUN ([ -f requirements.txt ] \
    && pip3 install --no-cache-dir -r requirements.txt) \
        || pip3 install --no-cache-dir jupyter jupyterlab

USER root

# Download the kernel release
RUN curl -L https://github.com/SpencerPark/IJava/releases/download/v1.3.0/ijava-1.3.0.zip > ijava-kernel.zip

# Unpack and install the kernel
RUN unzip ijava-kernel.zip -d ijava-kernel \
&& cd ijava-kernel \
&& python3 install.py --sys-prefix

# Set up the user environment

ENV NB_USER jovyan
ENV NB_UID 1000
ENV HOME /home/$NB_USER

RUN adduser --disabled-password \
    --gecos "Default user" \
    --uid $NB_UID \
    $NB_USER

COPY . $HOME

RUN chown -R $NB_UID $HOME

# Launch the notebook server
WORKDIR $HOME
RUN rm -rf *
RUN mkdir -p $HOME/work
CMD ["jupyter", "lab", "--ip", "0.0.0.0", "--allow-root"]