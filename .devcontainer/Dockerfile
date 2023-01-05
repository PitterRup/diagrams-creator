FROM python:3

WORKDIR /docs

RUN apt-get update \
 && apt-get install --no-install-recommends -y \
      graphviz \
      imagemagick \
      make \
      software-properties-common \
 && apt-add-repository 'deb http://security.debian.org/debian-security stretch/updates main' \ 
 && apt-get update \
 && apt-get install --no-install-recommends -y openjdk-8-jre \
 && apt-get autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

#PlantUML
ENV PLANTUML_DIR /usr/local/plantuml
ENV PLANTUML_JAR plantuml.jar
ENV PLANTUML $PLANTUML_DIR/$PLANTUML_JAR

RUN \
    echo "#PlantUML" && \
    mkdir $PLANTUML_DIR && \
    wget "https://sourceforge.net/projects/plantuml/files/plantuml.jar" --no-check-certificate && \
    echo "#Check jar file size. refs #9. normal jar file size is maybe > 5mb" && \
    size=$(stat -c %s plantuml.jar) && \
    test $size -gt 5000000 && \
    mv plantuml.jar $PLANTUML_DIR

COPY .devcontainer/requirements.txt .

RUN python3 -m pip install --no-cache-dir -U pip
RUN python3 -m pip install --no-cache-dir Pillow
RUN python3 -m pip install -r requirements.txt

CMD ["make", "html"]



#RUN apt-get install -y software-properties-common && \
#    add-apt-repository ppa:openjdk-r/ppa && \
#    apt-get update && \
#    apt-get install openjdk-8-jre