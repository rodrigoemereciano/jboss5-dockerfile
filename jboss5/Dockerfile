FROM centos:7


# Update OS and install required packages
##########################################
RUN yum -y update \
&& yum -y install git tar unzip wget \
&& yum clean all
 

# Install JAVA Oracle JDK 6u45
##########################################
COPY jdk6/jdk-6u45-linux-x64-rpm.bin /tmp/jdk-6u45-linux-x64-rpm.bin
RUN cd /tmp \
&& sh jdk-6u45-linux-x64-rpm.bin \
&& rm -rf /tmp/*
ENV JAVA_HOME /usr/java/default


# Install JBoss 5.1.0.GA
##########################################
RUN wget -O jboss.zip http://sourceforge.net/projects/jboss/files/JBoss/JBoss-5.1.0.GA/jboss-5.1.0.GA-jdk6.zip/download \
&& unzip jboss.zip \
&& mv jboss-5.1.0.GA /opt \
&& rm jboss.zip \
&& ln -s /opt/jboss-5.1.0.GA /opt/jboss \
&& cd /opt/jboss-5.1.0.GA/bin \
&& chmod +x *.sh
ENV JBOSS_HOME /opt/jboss

RUN ln -fs /usr/share/zoneinfo/America/Recife /etc/localtime 

# Run JBoss
##########################################
CMD ["/opt/jboss/bin/run.sh", "-b", "0.0.0.0"]

EXPOSE 8080
EXPOSE 8009