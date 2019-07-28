# Samuel Lee Toepke
# samueltoepke@gmail.com
# Summer 2019
# Dockerfile, CentOS 7
#
# Useful Commands:
# $ systemctl start docker
# $ docker ps # Running images
# $ docker images -a
# $ docker rmi -f $(docker images -q) # Delete all images
# $ docker build -t centos_7 .
# $ docker run -it centos_7
#
# Test Spring Boot Tomcat Application:
# $ docker ps # to get <container name>
# $ docker inspect <container name> | grep "IPAddress" # to get container IP address
# In browser from host (using IP address from above): 172.17.0.2:8080/gettime?tz=PST # to test web service
# 

# 0. Operating System
FROM centos:7

# 1. Set System Variables
ENV user newuser
ENV user_pwd newuser789
ENV main_java_app sprint-boot-time-web-service-1.0.jar
ENV startup startup.sh
ENV monit_log /var/log/monit.log

# 2. Set OpenJDK Variables
ENV open_jdk_dir_name jdk-12.0.2
ENV open_jdk_filename openjdk-12.0.2_linux-x64_bin.tar.gz
ENV open_jdk_link https://download.java.net/java/GA/jdk12.0.2/e482c34c86bd4bf8b56c0b35558996b9/10/GPL/openjdk-12.0.2_linux-x64_bin.tar.gz

# 3. Labels/Maintainer
LABEL project = "Docker CentOS 7, Spring Boot"
LABEL release-date = "2019-07-28"
MAINTAINER Samuel Toepke, samueltoepke@gmail.com

# 4. Start Firewall and Harden Installation
# All security is addressed by Docker daemon on host machine.

# 5. Create New, Non-Privileged User
RUN useradd -ms /bin/bash ${user}
RUN echo "${user}:${user_pwd}" | chpasswd

# 6. Install all Updates
RUN yum -y update

# 7. Install/Configure OpenJDK
RUN curl -sLO ${open_jdk_link}
RUN tar xvf ${open_jdk_filename}
RUN mv ${open_jdk_dir_name} /opt/
RUN echo export JAVA_HOME=/opt/${open_jdk_dir_name} >> /home/${user}/.bashrc 
RUN echo 'export PATH=$PATH:$JAVA_HOME/bin' >> /home/${user}/.bashrc 

# 8. Install Spring Boot Application
ADD ./${main_java_app} /home/${user}/${main_java_app}

# 9. Monit, Install
##RUN yum -y install epel-release
##RUN yum -y install monit

# 10. Monit, Set Permissions
##RUN chown ${user} /etc/monitrc
##RUN touch ${monit_log}
##RUN chown ${user} ${monit_log}

# 11. Add Startup File, Set Permissions
ADD ./${startup} /home/${user}/${startup}
RUN chmod +x /home/${user}/${startup}

# 12. Change to Non-Root User for Security/Safety
CMD /home/${user}/${startup}
USER ${user}
WORKDIR /home/${user}


