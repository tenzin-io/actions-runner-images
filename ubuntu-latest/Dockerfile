FROM summerwind/actions-runner-dind:v2.306.0-ubuntu-22.04

USER runner
RUN sudo apt-get update && \
    sudo apt-get install -y openssh-client && \
    sudo apt-get autoclean

# fix for 100% cpu utilization
# https://github.com/actions/runner/issues/2380
COPY --chown=runner:docker safe_sleep.sh /runnertmp/safe_sleep.sh
