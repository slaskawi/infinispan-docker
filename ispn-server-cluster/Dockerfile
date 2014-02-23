FROM centos
MAINTAINER vjuranek

RUN yum -y install unzip java-1.7.0-openjdk-devel
RUN wget http://downloads.jboss.org/infinispan/6.0.0.Final/infinispan-server-6.0.0.Final-bin.zip
RUN unzip infinispan-server-6.0.0.Final-bin.zip
RUN mkdir -p /opt/ispn
RUN mv ./infinispan-server-6.0.0.Final/* /opt/ispn
RUN sed -i 's/security-domain="other" auth-method="BASIC"//' /opt/ispn/standalone/configuration/clustered.xml

ENTRYPOINT /opt/ispn/bin/clustered.sh -b `ip a s | sed -ne '/127.0.0.1/!{s/^[ \t]*inet[ \t]*\([0-9.]\+\)\/.*$/\1/p}'`
