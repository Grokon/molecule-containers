ARG DEBIAN_VERSION=${DEBIAN_VERSION:-buster}

FROM docker.io/debian:${DEBIAN_VERSION}-slim

LABEL org.opencontainers.image.description="Debian 11 Container for Molecule"

# Install packages
RUN apt-get update \
    && apt-get -y install --no-install-recommends \
      systemd \
      systemd-sysv \
      sudo \
      procps \ 
      python3-pip \
      python3-dev \
      python3-setuptools \
      python3-wheel  \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/* \
    && rm -Rf /usr/share/doc && rm -Rf /usr/share/man \
    && pip3 install --upgrade pip \
    && pip3 install ansible-core ansible-lint cryptography \
    && mkdir -p /etc/ansible \
    && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts \
    && rm -f /lib/systemd/system/multi-user.target.wants/* \
      /etc/systemd/system/*.wants/* \
      /lib/systemd/system/local-fs.target.wants/* \
      /lib/systemd/system/sockets.target.wants/*udev* \
      /lib/systemd/system/sockets.target.wants/*initctl* \
      /lib/systemd/system/sysinit.target.wants/systemd-tmpfiles-setup* \
      /lib/systemd/system/systemd-update-utmp*
    
VOLUME ["/sys/fs/cgroup"]
CMD [ "/lib/systemd/systemd", "log-level=info", "unit=sysinit.target" ]
