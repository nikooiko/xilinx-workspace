FROM crops/poky

USER root

# Install Prerequisites (+ vim for interractive editing)
RUN apt-get -y update && apt-get -y install  \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common \
    jq \
    iptables \
    repo \
    vim

# Install Xilinx dependencies
ARG XILINX_BRANCH="rel-v2019.2"
ARG XILINX_INSTALL_PATH=/usr/local/xilinx
RUN install -o 1000 -g 1000 -d ${XILINX_INSTALL_PATH}
WORKDIR ${XILINX_INSTALL_PATH}
RUN repo init -u https://github.com/Xilinx/yocto-manifests.git \
    -b ${XILINX_BRANCH} \
    -m default.xml \
    && repo sync
ENV XILINX_INSTALL_PATH=${XILINX_INSTALL_PATH}

# Cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Create pokyuser
RUN ["/usr/bin/distro-entry.sh", "/usr/bin/dumb-init", "--", "/usr/bin/poky-entry.py"]

# Install builder scripts
COPY builder/scripts/* /usr/local/bin/

# Prepare for work directory
WORKDIR /workdir
RUN chown -R pokyuser:pokyuser /workdir
USER pokyuser
# Set Builder's paths. For now workdir is used for everything
ENV YOCTO_BUILD_DIR=/workdir/build/yocto-build \
    DL_DIR=/workdir/build/downloads \
    SSTATE_DIR=/workdir/build/sstate-cache

ENTRYPOINT ["/bin/bash"]