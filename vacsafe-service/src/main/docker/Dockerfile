# mvn clean package
# buildah bud -f vacsafe-service/src/main/docker/Dockerfile -t quay.io/redhat_naps_da/vacsafe-service:0.0.5 vacsafe-service
# podman push quay.io/redhat_naps_da/vacsafe-service:0.0.5

# https://github.com/Emergency-Response-Demo/container-images/tree/master/ubi8-java11-mvn
FROM quay.io/emergencyresponsedemo/ubi8-jdk-11-mvn:0.0.2

USER root

COPY target/repository /m2/repository

RUN chown -R 1001:0 /m2/repository \
  && chmod -R 776 /m2/repository

USER 1001

COPY target/*.jar /deployments/app.jar
