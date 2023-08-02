FROM summerwind/actions-runner-dind:v2.306.0-ubuntu-22.04

USER runner
RUN sudo apt-get update && \
    sudo apt-get install -y openssh-client python3-pip gpg lsb-release wget

# Install Ansible
RUN pip install --upgrade pip && \
    pip install --upgrade ansible && \
    ansible-galaxy collection install --timeout 180 community.general && \
    ansible --version

# Install Hashicorp's Vault
RUN wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list && \
    sudo apt-get update && \
    sudo apt-get install -y vault && \
    vault version

RUN sudo apt-get autoclean

# fix for 100% cpu utilization
# https://github.com/actions/runner/issues/2380
COPY --chown=runner:docker safe_sleep.sh /runnertmp/safe_sleep.sh
