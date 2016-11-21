# tomcat-rhel-base

A secure, non-s2i tomcat8/rhel7.2 based image which can be used as a base image for j2ee tomcat apps.

Specs:
Size – 407.9 MB
Vulnerabilities – Passed

---


#Dockerfile for testing with J2EE app - 

 
# Base Image
FROM containers.cisco.com/dhsanghv/tomcat-rhel
 
# Maintainer
MAINTAINER dhsanghv
 
# Copy Deployment File (can use ADD as well in place of COPY)
COPY ./target/*.war /opt/tomcat/webapps/
 
RUN echo "Building Image, Bro!"
 
# Port Setup
EXPOSE 8080
 
# Recursively grant ownership of the directory /opt/tomcat, and all files and subdirectories, to user root.
RUN chown -R root:root /opt/tomcat &&\
    chmod -R g+rw /opt/tomcat 
 
# Main Command
CMD ["/opt/tomcat/bin/catalina.sh", "run"]