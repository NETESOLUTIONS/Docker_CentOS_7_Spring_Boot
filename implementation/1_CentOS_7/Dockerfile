# Samuel Lee Toepke
# samueltoepke@gmail.com
# Winter 2019
# Dockerfile, CentOS 7.
# $ systemctl start docker
# $ docker ps
# $ docker images -a
# $ docker rmi -f $(docker images -q) # Delete all images
# $ docker build -t centos7 .
# $ docker run -it centos7

# 0. Operating System
FROM centos:7

# 1. Labels/Maintainer
LABEL project="Docker CentOS 7"
LABEL release-date="2019-12-27"
MAINTAINER Samuel Toepke, samueltoepke@gmail.com

# 2. Start Firewall
# Don't have to configure firewall, addressed by Docker daemon.
  
# 3. Install all Updates and EPEL
RUN yum -y update 
RUN yum -y install epel-release
