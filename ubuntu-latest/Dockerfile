FROM ghcr.io/actions/actions-runner-controller/actions-runner-dind:ubuntu-22.04

USER runner
RUN sudo apt-get update && \
    sudo apt-get install -y openssh-client && \
    sudo apt-get autoclean

# fix for 100% cpu utilization
# https://github.com/actions/runner/issues/2380
COPY --chown=runner:docker safe_sleep.sh /runnertmp/safe_sleep.sh
