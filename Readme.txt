FROM jenkins/jenkins
USER root
RUN apt-get update && apt-get install -g docker-ce-cli
RUN apt-get update && apt-get install -g lsb-release
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
USER jenkins

#jenkins image used

#docker build -t jenkins-docker .

docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -d -v jenkins_home:/var/jenkins_home jenkins-docker
to Unlock jenkins and get admin password in windows

docker logs jenkins-docker