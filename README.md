# Docker, CentOS 7, OpenJDK 12, Spring Boot
This is an example Dockerfile showing functionality of deploying a Spring Boot Java JAR file using CentOS 7. 

Upon building of the container, the following are installed/configured:
* All updates/upgrades.
* OpenJDK 12.
* The target JAR file.

The JAR file will run when the container is started.

There is some commented-out code pertaining to Monit...next steps.

The eventual goal is to port to RedHat 7. CentOS will provide a good enough sandbox for now.

## Instructions:
Follow notes in the comments at the top of `./implementation/Dockerfile`.
