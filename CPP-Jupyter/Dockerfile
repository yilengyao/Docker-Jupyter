FROM ubuntu:18.04
# Java 8 (Oracle) Dockerfile
# Base image: Ubuntu
# Installs: Java 8

# Install basic software support
RUN apt-get update

RUN apt-get update
RUN apt-get install -y python3-pip && \
    apt-get install -y curl unzip wget


# add requirements.txt, written this way to gracefully ignore a missing file
COPY . .
RUN ([ -f requirements.txt ] \
    && pip3 install --no-cache-dir -r requirements.txt) \
        || pip3 install --no-cache-dir jupyter jupyterlab

# Anaconda installing
RUN wget https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
RUN bash Anaconda3-5.0.1-Linux-x86_64.sh -b && \
    echo "export PATH="/root/anaconda3/bin:$PATH"" >> ~/.bashrc && \
    /bin/bash -c "source ~/.bashrc"
RUN rm Anaconda3-5.0.1-Linux-x86_64.sh




# Set path to conda
#ENV PATH /root/anaconda3/bin:$PATH
ENV PATH /root/anaconda3/bin:$PATH

# Updating Anaconda packages
# RUN conda update conda
RUN conda update anaconda
# RUN conda update --all

RUN conda install xeus-cling -c conda-forge

# Set up the user environment
USER root

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