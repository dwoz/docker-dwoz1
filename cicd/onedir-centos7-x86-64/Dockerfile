FROM centos:7

WORKDIR /
RUN yum -y install \
    deltarpm \
    epel-release \
  && yum --disablerepo="*" --enablerepo="epel" list available \
  && yum -y install yum-utils \
  && yum repolist \
  && yum makecache \
  && yum -y groupinstall "Development Tools" \
  && yum-builddep -y python3 \
  && yum -y install \
    zlib-devel \
    patchelf \
  && yum clean all \
  && rm -rf /var/cache/yum

LABEL \
  maintainer="Daniel Wozniak <dwozniak@vmware.com>" \
  io.saltproject.name="Onedir Centos 7 Build Container" \
  io.saltproject.url="https://github.com/dwoz/docker-dwoz1"
