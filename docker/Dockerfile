# I N F R A
# Dockerfile with SteamRT3 
FROM        registry.gitlab.steamos.cloud/steamrt/sniper/sdk 
LABEL       author="Liam C" maintainer="infra@gflclan.com"
LABEL       org.opencontainers.image.source="https://github.com/1zc/cs2-pterodactyl"

# Libs
RUN        apt-get update
RUN        apt-get install -y zlib1g libzstd1 libmariadb3

# MariaDB c++ connector
RUN wget https://dlm.mariadb.com/2531499/Connectors/cpp/connector-cpp-1.0.2/mariadb-connector-cpp-1.0.2-debian-bullseye-amd64.tar.gz
RUN tar -xvzf mariadb-connector-cpp-*.tar.gz
RUN install -d /usr/include/mariadb/conncpp
RUN install -d /usr/include/mariadb/conncpp/compat
RUN install /tmp/mariadb-connector-cpp-*/include/mariadb/* /usr/include/mariadb/ || true
RUN install /tmp/mariadb-connector-cpp-*/include/mariadb/conncpp/* /usr/include/mariadb/conncpp || true
RUN install /tmp/mariadb-connector-cpp-*/include/mariadb/conncpp/compat/* /usr/include/mariadb/conncpp/compat || true
RUN install -d /usr/lib/mariadb
RUN install -d /usr/lib/mariadb/plugin
RUN install /tmp/mariadb-connector-cpp-*/lib/mariadb/libmariadbcpp.so /usr/lib || true
RUN install /tmp/mariadb-connector-cpp-*/lib/mariadb/plugin/* /usr/lib/mariadb/plugin || true

# Prep OS
RUN         mkdir -p /etc/sudoers.d && echo "%sudo ALL=(ALL:ALL) NOPASSWD: ALL" > /etc/sudoers.d/flatdeb && chmod 0440 /etc/sudoers.d/flatdeb
ENV         DEBIAN_FRONTEND=noninteractive
USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

# To-Do: If CS2 requires Wine, the following lines will need to be uncommented
# RUN         apt update
# RUN         apt install -y wine wine64 libwine && apt clean

# EP
COPY        ./docker/entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]

