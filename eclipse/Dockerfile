FROM vintec/basejava:v8
MAINTAINER Isidoro Trevino "isidoro.trevino@vintec.mx"


RUN wget http://mirror.csclub.uwaterloo.ca/eclipse/technology/epp/downloads/release/oxygen/M6/eclipse-jee-oxygen-M6-linux-gtk-x86_64.tar.gz -O /tmp/eclipse.tar.gz -q && \
    echo 'Installing eclipse' && \
    sudo apt-get update && sudo apt-get install -y libgtk2.0-0 libcanberra-gtk-module && \
    sudo tar -xf /tmp/eclipse.tar.gz -C /opt && \
    rm /tmp/eclipse.tar.gz

ADD run /usr/local/bin/eclipse

COPY ["files/features.txt", "files/repositories.txt", "files/prepare_eclipse.sh", "/tmp/files/"]

USER root

RUN chmod +x /usr/local/bin/eclipse && \
    mkdir -p /home/developer && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown root:root /usr/bin/sudo && \
    chmod 4755 /usr/bin/sudo && \
    ls -la /tmp && \
    ls -la /tmp/files && \
    chmod 755 /tmp/files/*.sh && \
	wget http://spring-roo-repository.springsource.org.s3.amazonaws.com/release/ROO/spring-roo-1.3.2.RELEASE.zip -O /opt/springroo.zip -q && \
	unzip /opt/springroo.zip && \
    wget http://central.maven.org/maven2/org/projectlombok/lombok/1.16.16/lombok-1.16.16.jar -O /tmp/files/lombok.jar && \
	java -jar /tmp/files/lombok.jar install /opt/eclipse && \
    /tmp/files/prepare_eclipse.sh /opt/eclipse && \
	chown -R developer:developer /opt/ && \
    chown developer:developer -R /home/developer && \
    rm -rf /tmp/* && \
	rm -rf /opt/springroo.zip

USER developer
ENV HOME /home/developer
WORKDIR /home/developer
CMD /usr/local/bin/eclipse

