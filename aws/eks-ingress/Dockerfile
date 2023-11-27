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

RUN npm install