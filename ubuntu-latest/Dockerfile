FROM summerwind/actions-runner-dind:v2.307.1-ubuntu-22.04

ARG VAULT_VERSION=1.14.1

USER runner
RUN sudo apt-get update && \
    sudo apt-get install -y openssh-client python3-pip gpg lsb-release curl unzip

# Install Ansible
RUN pip install --upgrade pip && \
    pip install --upgrade ansible && \
    pip install --upgrade hvac && \
    ansible-galaxy collection install --timeout 180 community.general && \
    ansible-galaxy collection install --timeout 180 community.hashi_vault && \
    ansible --version

# Install Hashicorp's Vault
RUN sudo curl -s -L -o /tmp/vault.zip https://releases.hashicorp.com/vault/${VAULT_VERSION}/vault_${VAULT_VERSION}_linux_amd64.zip && \
    unzip /tmp/vault.zip -d /home/runner/.local/bin/ && \
    vault version

RUN sudo apt-get autoclean

# fix for 100% cpu utilization
# https://github.com/actions/runner/issues/2380
COPY --chown=runner:docker safe_sleep.sh /runnertmp/safe_sleep.sh
