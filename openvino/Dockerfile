FROM ubuntu:18.04
LABEL maintainer="bpdp@akakom.ac.id"
# Taken from: https://github.com/cortexica/openvino
# updated to 2019-R1.1

RUN apt-get -y update && apt-get install -y --no-install-recommends \
        lsb-release \
        cpio \
        sudo \
        wget \
    && rm -rf /var/lib/apt/lists/*

# Download and install OpenVino 2019-R1.1
RUN wget -nv -O /tmp/openvino.tar.gz http://registrationcenter-download.intel.com/akdlm/irc_nas/15512/l_openvino_toolkit_p_2019.1.144.tgz \
    && tar -xzf /tmp/openvino.tar.gz -C /tmp \
    && rm /tmp/openvino.tar.gz \
    && cd /tmp/l_openvino_toolkit_p_2019.1.144  \
    && sed -i 's/^\(ACCEPT_EULA\)=.*$/\1=accept/' silent.cfg \
    && echo "Installing OpenVino..." \
    && ./install.sh -s silent.cfg \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*

# Set default runtime to python3
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 10
ENV PYTHONPATH=${PYTHONPATH}:/opt/intel/openvino/python/python3.6

# Append library path
ENV LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/opt/intel/openvino/deployment_tools/inference_engine/lib/intel64

ADD demo.sh .
