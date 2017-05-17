FROM vintec/basejava:v8
MAINTAINER Isidoro Trevino "isidoro.trevino@vintec.mx"

RUN wget https://github.com/aptana/studio3/releases/download/v3.6.1/Aptana_Studio_3_Setup_Linux_x86_64_3.6.1.zip -O /tmp/eclipse.zip -q && \
    echo 'Installing eclipse' && \
    sudo unzip /tmp/eclipse.zip -d /opt && \
    rm /tmp/eclipse.zip && \
    sudo apt-get update && sudo apt-get install -y libgtk2.0-0 libcanberra-gtk-module

ADD run /usr/local/bin/eclipse

RUN sudo chown -R developer:developer /opt/ && \
    sudo chmod +x /usr/local/bin/eclipse

USER developer
ENV HOME /home/developer
WORKDIR /home/developer
CMD /usr/local/bin/eclipse

