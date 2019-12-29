# Samuel Lee Toepke
# samueltoepke@gmail.com
# Winter 2019
# Dockerfile, CentOS 7, AWS Corretto.
# $ systemctl start docker
# $ docker ps
# $ docker images -a
# $ docker rmi -f $(docker images -q) # Delete all images
# $ docker build -t centos7-corretto .
# $ docker run -it centos7-corretto

# 0. Operating System
FROM centos:7

# 1. Labels/Maintainer
LABEL project="Docker CentOS 7"
LABEL release-date="2019-12-27"
MAINTAINER Samuel Toepke, samueltoepke@gmail.com

# 2. Environment Variables
ENV corretto_11_link https://corretto.aws/downloads/latest/amazon-corretto-11-x64-linux-jdk.rpm
ENV corretto_11_filename amazon-corretto-11-x64-linux-jdk.rpm

# 3. Start Firewall
# Don't have to configure firewall, addressed by Docker daemon.
  
# 4. Install all Updates and EPEL
RUN yum -y update 
RUN yum -y install epel-release

# 5. Install AWS Corretto 11 JDK 
RUN curl -sLO ${corretto_11_link}
RUN rpm -i ${corretto_11_filename}
RUN rm -rf ${corretto_11_filename}
