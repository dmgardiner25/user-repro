FROM  mcr.microsoft.com/devcontainers/base:jammy

RUN apt-get update \
    && apt-get install --no-install-recommends -y rsyslog systemd systemd-cron \
    && rm -f /usr/local/bin/systemctl \
    && apt-get clean

CMD ["/lib/systemd/systemd", "--system", "--unit=basic.target"]