FROM mcr.microsoft.com/devcontainers/cpp:1-debian-12

ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="none"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/

RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# Add Ubuntu Toolchain PPA sources to apt
COPY ./ubuntu-toolchain-r.sources /etc/apt/sources.list.d/ubuntu-toolchain-r.sources

# [Optional] Uncomment this section to install additional packages.
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends gcc-13 g++-13 ltrace

# Setup GCC-13 as default compiler version
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-13 30 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-13 30