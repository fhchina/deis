FROM ubuntu-debootstrap:14.04

ENV DEBIAN_FRONTEND noninteractive

# install common packages
RUN apt-get update && apt-get install -y curl net-tools sudo

# install etcdctl
RUN curl -sSL -o /usr/local/bin/etcdctl https://s3-us-west-2.amazonaws.com/opdemand/etcdctl-v0.4.6 \
    && chmod +x /usr/local/bin/etcdctl

# install confd
RUN curl -sSL -o /usr/local/bin/confd https://github.com/kelseyhightower/confd/releases/download/v0.8.0/confd-0.8.0-linux-amd64 \
    && chmod +x /usr/local/bin/confd

ADD build.sh /tmp/build.sh
RUN DOCKER_BUILD=true /tmp/build.sh

# define the execution environment
WORKDIR /app
CMD ["/app/bin/boot"]
EXPOSE 5432
ADD . /app

ENV DEIS_RELEASE 1.5.0-dev

