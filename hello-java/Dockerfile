FROM   registry.access.redhat.com/ubi8/ubi:8.0

MAINTAINER   Red Hat Training <training@redhat.com>

# command line options to pass to the JVM
ENV	  JAVA_OPTIONS -Xmx512m


# Install the Java runtime, create a user for running the app, and set permissions
RUN   yum install -y --disableplugin=subscription-manager java-1.8.0-openjdk-headless && \
      yum clean all --disableplugin=subscription-manager -y && \
      mkdir -p /opt/app-root/bin

# Copy the runnable fat JAR to the container.
ADD   https://github.com/RedHatTraining/DO288-apps/releases/download/OCP-4.1-1/hello-java.jar /opt/app-root/bin/

COPY  run-app.sh /opt/app-root/bin/

RUN   chgrp -R 0 /opt/app-root && \
      chmod -R g=u /opt/app-root

EXPOSE 8080

# Replace the wildfly user in the USER instruction on line 24 with the generic userid of 1001 to avoid inheriting the user from the parent RHEL image. This generic userid is ignored by OpeShift and follows RedHatrecommendations and conventions for building images:
USER  1001

# Run the fat JAR
CMD   /opt/app-root/bin/run-app.sh
