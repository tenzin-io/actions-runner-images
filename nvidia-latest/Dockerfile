FROM summerwind/actions-runner-dind:v2.308.0-ubuntu-22.04

USER runner

# safe_sleep.sh fix for 100% cpu utilization
# https://github.com/actions/runner/issues/2380
COPY --chown=runner:docker safe_sleep.sh /runnertmp/safe_sleep.sh

# install system packages
RUN sudo apt-get update && \
    sudo apt-get install -y curl python3 python3-pip tesseract-ocr openssh-client && \
    sudo apt-get autoclean && \
    sudo pip install -U pip

# install conda
RUN curl -o /tmp/conda_installer.sh https://repo.anaconda.com/archive/Anaconda3-2023.03-Linux-x86_64.sh && \
    chmod +x /tmp/conda_installer.sh && \
    bash /tmp/conda_installer.sh -b -f
RUN ~/anaconda3/bin/conda install -c conda-forge cudatoolkit=11.8.0 -q -y

COPY requirements.txt .
RUN python3 -m pip install -r requirements.txt

USER root

# update ld_library search path
RUN echo "/home/runner/anaconda3/lib/" > /etc/ld.so.conf.d/nvidia.conf && \
    echo "/home/runner/.local/lib/python3.10/site-packages/nvidia/cudnn/lib" >> /etc/ld.so.conf.d/nvidia.conf

USER runner
