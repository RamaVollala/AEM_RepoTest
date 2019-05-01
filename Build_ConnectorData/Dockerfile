FROM aem_maven:latest

#Get the code

ADD sw-aem-connector-data/it.launcher/pom.xml /sw-aem-connector-data/it.launcher/pom.xml
ADD sw-aem-connector-data/core/pom.xml /sw-aem-connector-data/core/pom.xml
ADD sw-aem-connector-data/pom.xml /sw-aem-connector-data/pom.xml
ADD sw-aem-connector-data/it.tests/pom.xml /sw-aem-connector-data/it.tests/pom.xml
ADD sw-aem-connector-data/core.gen/pom.xml /sw-aem-connector-data/core.gen/pom.xml
ADD sw-aem-connector-data/build-tools/pom.xml /sw-aem-connector-data/build-tools/pom.xml
ADD sw-aem-connector-data/ui.apps/pom.xml /sw-aem-connector-data/ui.apps/pom.xml
ADD sw-aem-connector-data/core.gen/src/main/resources/swagger/ /sw-aem-connector-data/core.gen/src/main/resources/swagger/
ADD sw-aem-connector-data/core.gen/src/main/resources/jsonschema2pojo/ /sw-aem-connector-data/core.gen/src/main/resources/jsonschema2pojo/
ADD sw-aem-connector-data/build-tools/src/main/resources/sherwinaem/pmd-ruleset.xml /sw-aem-connector-data/build-tools/src/main/resources/sherwinaem/pmd-ruleset.xml


RUN cd /sw-aem-connector-data

RUN mvn --fail-at-end clean install package -PautoInstallBundleArtifactory $proxy_config; \
  mvn --settings core.gen/settings.xml --fail-at-end versions:set -DnewVersion=1.0.0-SNAPSHOT -PautoInstallBundleArtifactory $proxy_config; \
  find /sw-aem-connector-data/ -maxdepth 3 -type d -name target|xargs rm -rf; exit 0
