#FROM jenkins/jenkins:lts
FROM jenkins/jenkins

#Take the host docker groupid
ARG HOST_DOCKER_GID=998

# if we want to install via apt
USER root

# install dependencies to use the hosts docker socket
RUN apt-get update && \
apt-get -y install apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common && \
curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
   $(lsb_release -cs) \
   stable" && \
apt-get update && \
apt-get -y install docker-ce

# install dependencies to build .net core apps
RUN apt-get update && apt-get install -y libunwind8 libicu58

# install lftp to publish files over FTP
RUN apt-get install -y lftp

# set docker permissions
RUN groupmod -g $HOST_DOCKER_GID docker
RUN usermod -aG docker jenkins

# drop back to the regular jenkins user - good practice
USER jenkins
