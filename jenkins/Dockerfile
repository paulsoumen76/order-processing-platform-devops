FROM jenkins/jenkins:lts-jdk21

USER root

# Basic tools
RUN apt-get update && \
    apt-get install -y \
        curl \
        ca-certificates \
        git \
        unzip \
        && \
    rm -rf /var/lib/apt/lists/*

# Install Docker CLI
RUN curl -fsSL https://download.docker.com/linux/debian/gpg \
        -o /usr/share/keyrings/docker.asc && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.asc] https://download.docker.com/linux/debian \
        $(. /etc/os-release && echo "$VERSION_CODENAME") stable" \
        > /etc/apt/sources.list.d/docker.list && \
    apt-get update && \
    apt-get install -y docker-ce-cli && \
    rm -rf /var/lib/apt/lists/*

# Install kubectl
RUN KUBECTL_VERSION=$(curl -L -s https://dl.k8s.io/release/stable.txt) && \
    curl -LO "https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Jenkins plugins needed for our CI/CD system
RUN jenkins-plugin-cli --plugins \
    workflow-aggregator \
    git \
    github \
    credentials-binding \
    docker-workflow \
    junit \
    pipeline-stage-view

USER root