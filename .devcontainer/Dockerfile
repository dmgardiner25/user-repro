FROM mcr.microsoft.com/devcontainers/universal:2-focal

RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

RUN apt-get update && apt-get install -y \
   "build-essential" \
   "g++" \
   "openjdk-11-jdk"                \
   "amazon-ecr-credential-helper"  \
   "jq"                            \
   "gnutls-dev"                    \
   "libcrypto++-dev"               \
   "systemtap-sdt-dev"             \
   "xfslibs-dev"                   \
   "valgrind"                      \
   "automake"                      \
   "libtool" \
   "vagrant" \
   "packer" \
   "terraform" \
   "iputils-ping" \
   "dnsutils"

RUN NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

ENV PATH="/home/linuxbrew/.linuxbrew/bin:${PATH}"

RUN brew install datreeio/datree/datree duf aviator-co/tap/av
RUN go install github.com/bazelbuild/buildtools/buildifier@latest && \
      go install github.com/google/wire/cmd/wire@latest && \
      go install mvdan.cc/gofumpt@latest

RUN npm install -g vercel npm-check-updates gtop

# Install Bazelisk
ARG BAZELISK_VERSION=v1.15.0
ARG BAZELISK_DOWNLOAD_SHA=dev-mode
RUN curl -fSsL -o /usr/local/bin/bazelisk https://github.com/bazelbuild/bazelisk/releases/download/${BAZELISK_VERSION}/bazelisk-linux-amd64 \
    && ([ "${BAZELISK_DOWNLOAD_SHA}" = "dev-mode" ] || echo "${BAZELISK_DOWNLOAD_SHA} */usr/local/bin/bazelisk" | sha256sum --check - ) \
    && chmod 0755 /usr/local/bin/bazelisk

