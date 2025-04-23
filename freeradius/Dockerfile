# Use official Ubuntu base image
ARG DEBIAN_FRONTEND=noninteractive
FROM ubuntu:22.04
# Install necessary tools
RUN apt-get update && apt-get install -y \
    wget \
    gpg \
    apt-transport-https \
    ca-certificates \
    gnupg
# Import NetKnights GPG key and add repository
RUN wget https://lancelot.netknights.it/NetKnights-Release.asc && \
    gpg --dearmor -o /usr/share/keyrings/netknights.gpg NetKnights-Release.asc && \
    echo "deb [signed-by=/usr/share/keyrings/netknights.gpg] http://lancelot.netknights.it/community/jammy/stable jammy main" \
    > /etc/apt/sources.list.d/netknights.list && \
    rm NetKnights-Release.asc
# Prevent services from starting during install
RUN echo '#!/bin/sh\nexit 101' > /usr/sbin/policy-rc.d && chmod +x /usr/sbin/policy-rc.d
# ⚠️ Dummy systemctl to avoid post-install failure
RUN echo -e '#!/bin/sh\nexit 0' > /bin/systemctl && chmod +x /bin/systemctl
# Install privacyidea-radius
RUN apt-get update && \
    apt-get install -y --no-install-recommends privacyidea-radius && \
    rm /usr/sbin/policy-rc.d && \
    rm /bin/systemctl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

