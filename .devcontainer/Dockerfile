FROM ubuntu:20.04

# Enable new "BUILDKIT" mode for Docker CLI
ENV DOCKER_BUILDKIT=1

# Remove apt-get prompt for timezone
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        git \
        ruby \
        bash-completion \
        wget \
        ca-certificates \
        python3-pip \
        clang-tidy \
    # Clean up
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# Install kitware repo to get latest CMake (required wget)
RUN wget -qO /etc/apt/trusted.gpg.d/kitware-key.asc https://apt.kitware.com/keys/kitware-archive-latest.asc \
    && echo "deb https://apt.kitware.com/ubuntu/ focal main" | tee /etc/apt/sources.list.d/kitware.list \
    export DEBIAN_FRONTEND=noninteractive \
    && apt-get update && apt-get install -y --no-install-recommends \
        cmake \
    # Clean up
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts/

# Install ninja to get fast build
RUN wget -qO /usr/local/bin/ninja.gz https://github.com/ninja-build/ninja/releases/latest/download/ninja-linux.zip \
    && gunzip /usr/local/bin/ninja.gz \
    && chmod a+x /usr/local/bin/ninja

# Install ceedling (required ruby) to run automated tests
RUN gem install ceedling

# Install conan
RUN pip install conan==2.0.0b6
