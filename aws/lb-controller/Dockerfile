FROM pulumi/pulumi-nodejs
ARG TARGETPLATFORM

COPY . .

# Install the aws cli
RUN case "${TARGETPLATFORM}" in \
         "linux/amd64")  CLI_URL="https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" ;; \
         "linux/arm64")  CLI_URL="https://awscli.amazonaws.com/awscli-exe-linux-aarch64.zip" ;; \
         *) exit 1 ;; \
    esac; \
    curl $CLI_URL -o "awscliv2.zip" \
    && apt-get install zip -y \
    && unzip -u awscliv2.zip \
    && ./aws/install \
    && mv /usr/local/bin/aws /bin/aws \
    && aws --version

# Install eksctl to install IAM policy and service account
RUN curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_Linux_amd64.tar.gz" \
    && tar -xzf eksctl_Linux_amd64.tar.gz -C /tmp && rm eksctl_Linux_amd64.tar.gz \
    && mv /tmp/eksctl /usr/bin \
    && eksctl version

RUN npm install