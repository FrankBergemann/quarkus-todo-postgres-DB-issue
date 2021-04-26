####
# This Dockerfile is used in order to build a container that runs the Quarkus application in JVM mode
#
# Before building the docker image run:
#
# mvn package
#
# Then, build the image with:
#
# docker build -f src/main/docker/Dockerfile.jvm -t quarkus/todo-backend-jvm .
#
# Then run the container using:
#
# docker run -i --rm -p 8080:8080 quarkus/todo-backend-jvm
#
###
FROM azul/zulu-openjdk-alpine:11

LABEL Frank Bergemann <frank.bergemann@nttdata.com>

USER root

RUN apk --no-cache add curl

ENV JAVA_OPTIONS="-Dquarkus.http.host=0.0.0.0 -Djava.util.logging.manager=org.jboss.logmanager.LogManager"
ENV AB_ENABLED=jmx_exporter

# Be prepared for running in OpenShift too
RUN mkdir /deployments
RUN adduser -G root --no-create-home --disabled-password 1001 \
  && chown -R 1001 /deployments \
  && chmod -R "g+rwX" /deployments \
  && chown -R 1001:root /deployments

COPY target/lib/* /deployments/lib/
COPY target/*-runner.jar /deployments/app.jar
EXPOSE 8080

# run with user 1001
USER 1001

#ENTRYPOINT [ "/deployments/run-java.sh" ]
CMD ["sh", "-c", "cd /deployments; java -jar app.jar"]

## create containerized quarkus todo application
#RUN mkdir -p /usr/share/quarkus
#COPY quarkus-target.tar.gz /usr/share/quarkus
#RUN tar -xzf /usr/share/quarkus/quarkus-target.tar.gz -C /usr/share/quarkus
#RUN rm -f /usr/share/quarkus/quarkus-target.tar.gz
#
#EXPOSE 8080
#
#CMD ["sh", "-c", "cd /usr/share/quarkus; java -jar target/todo-backend-1.0-SNAPSHOT-runner.jar"]