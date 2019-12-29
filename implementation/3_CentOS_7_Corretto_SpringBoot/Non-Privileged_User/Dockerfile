# Samuel Lee Toepke
# samueltoepke@gmail.com
# Winter 2019
# Dockerfile, CentOS 7, AWS Corretto, Sprint Boot JAR.
#   Performs actions as a non-privileged user.
# $ systemctl start docker
# $ docker ps
# $ docker images -a
# $ docker rmi -f $(docker images -q) # Delete all images
# $ docker build -t centos7-corretto-sb .
#
# To automatically start JAR file on container run:
#   $ docker run -p 8080:8080 centos7-corretto-sb
#
# To manually start JAR file on container run:
#   * Comment the CMD in Step 7 below.
#   $ docker run -p 8080:8080 -it centos7-corretto-sb
#     --> $ java -jar /home/newuser/sprint-boot-time-web-service-1.0.jar
#
# To test in host browser: 
#   * http://localhost:8080/gettime
#   * http://localhost:8080/gettime?tz=EST

# 0. Operating System.
FROM centos:7

# 1. Labels/Maintainer.
LABEL project="Docker CentOS 7, Corretto, Spring Boot"
LABEL release-date="2019-12-27"
MAINTAINER Samuel Toepke, samueltoepke@gmail.com

# 2. Environment Variables.
ENV corretto_11_link https://corretto.aws/downloads/latest/amazon-corretto-11-x64-linux-jdk.rpm
ENV corretto_11_filename amazon-corretto-11-x64-linux-jdk.rpm
ENV main_java_app sprint-boot-time-web-service-1.0.jar
ENV user newuser
ENV user_pwd newuser789

# 3. Start Firewall.
# Don't have to configure firewall, addressed by Docker daemon.
  
# 4. Install all Updates and EPEL.
RUN yum -y update 
RUN yum -y install epel-release

# 5. Install AWS Corretto 11 JDK.
RUN curl -sLO ${corretto_11_link}
RUN rpm -i ${corretto_11_filename}
RUN rm -rf ${corretto_11_filename}

# 6. Install Spring Boot JAR.
ADD ./${main_java_app} /home/${user}/${main_java_app}
RUN chmod 755 /home/${user}/${main_java_app}

# 7. Create New, Non-Privileged User
RUN useradd -ms /bin/bash ${user}
RUN echo "${user}:${user_pwd}" | chpasswd

# 8. Change user, run Spring Boot JAR on container start.
USER ${user}
WORKDIR /home/${user}
CMD java -jar /home/${user}/${main_java_app}
