FROM aem_maven:latest

#Get the code

ADD sw-aem-foundation-core/it.launcher/pom.xml /sw-aem-foundation-core/it.launcher/pom.xml
ADD sw-aem-foundation-core/core/pom.xml /sw-aem-foundation-core/core/pom.xml
ADD sw-aem-foundation-core/pom.xml /sw-aem-foundation-core/pom.xml
ADD sw-aem-foundation-core/ui.businesslogic/pom.xml /sw-aem-foundation-core/ui.businesslogic/pom.xml
ADD sw-aem-foundation-core/it.tests/pom.xml /sw-aem-foundation-core/it.tests/pom.xml
ADD sw-aem-foundation-core/build-tools/pom.xml /sw-aem-foundation-core/build-tools/pom.xml
ADD sw-aem-foundation-core/ui.apps/pom.xml /sw-aem-foundation-core/ui.apps/pom.xml

RUN cd /sw-aem-foundation-core && mvn --fail-at-end clean install package -PautoInstallBundleArtifactory $proxy_config; \
  mvn --settings settings.xml --fail-at-end versions:set -DnewVersion=1.0.0-SNAPSHOT -PautoInstallBundleArtifactory $proxy_config; \
  find /sw-aem-foundation-core/ -maxdepth 3 -type d -name target|xargs rm -rf; exit 0
