FROM ubuntu

RUN echo "root:smsn" | chpasswd

# where to mount data
RUN mkdir /mnt/smsn-data

# choose a character set
RUN apt-get clean && apt-get update
RUN apt-get install locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

# misc prerequisites
RUN apt update
RUN apt install -y git wget unzip maven vim
RUN apt install -y default-jre default-jdk # java
RUN apt install -y tcpdump net-tools locales # python # maybe not needed

# # python's web library
# WORKDIR /root
# RUN wget http://webpy.org/static/web.py-0.38.tar.gz
# RUN tar -xvzf web.py-0.38.tar.gz && rm web.py-0.38.tar.gz
# WORKDIR /root/web.py-0.38
# RUN python setup.py install

# gremlin: install, and build the neo4j plugin for it
WORKDIR /root
COPY apache-tinkerpop-gremlin-server-3.4.2 /root/apache-tinkerpop-gremlin-server-3.4.2
WORKDIR /root/apache-tinkerpop-gremlin-server-3.4.2
RUN ln -s /root/apache-tinkerpop-gremlin-server-3.4.2 /root/gremlin

RUN /root/gremlin/bin/gremlin-server.sh install org.apache.tinkerpop neo4j-gremlin 3.4.2

EXPOSE 8182

WORKDIR /root/gremlin
CMD ["/bin/bash"]
