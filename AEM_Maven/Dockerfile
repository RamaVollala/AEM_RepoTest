FROM docker.cpartdc01.sherwin.com/ecomm/apps/aem_java:latest

ARG proxy_config
#Install Maven

RUN cd /usr/local \
  && curl 'https://repo.maven.apache.org/maven2/org/apache/maven/apache-maven/3.5.3/apache-maven-3.5.3-bin.tar.gz' -o apache-maven-3.5.3-bin.tar.gz \
  && tar -xzf apache-maven-3.5.3-bin.tar.gz \
  && rm apache-maven-3.5.3-bin.tar.gz \
  && ln -s apache-maven-3.5.3  maven \
  && echo "export M2_HOME=/usr/local/maven" >> /etc/profile.d/maven.sh \
  && echo "export PATH=\${M2_HOME}/bin:\${PATH}" >> /etc/profile.d/maven.sh

#Install Gradle
RUN yum -y install unzip \
  && curl -L https://services.gradle.org/distributions/gradle-4.9-bin.zip -o /tmp/gradle-4.9-bin.zip \
  && ls -al /tmp \
  && mkdir /opt/gradle \
  && unzip -d /opt/gradle /tmp/gradle-4.9-bin.zip \
  && rm /tmp/gradle-4.9-bin.zip \
  && echo "export PATH=$PATH:/opt/gradle/gradle-4.9/bin" >> /etc/profile.d/gradle.sh

SHELL ["/bin/bash","--login", "-c"]
