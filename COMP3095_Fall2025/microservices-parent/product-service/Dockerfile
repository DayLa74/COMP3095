#----------------
# Build Stage
#----------------

FROM gradle:8-jdk-21 as builder
COPY --chown=gradle:gradle ../.. /home/gradle/src

WORKDIR /home/gradle/src

RUN ./gradle build -k test -

#----------------
# Package Stage
#----------------

from openjdk:21-jdk

RUN mkdir /app

copy --frombuilder /home/gradle/src/build/libs/*.jar /app/

ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PASSWORD=password

EXPOSE 8084
ENTRYPOINT ["java", "jar", "/app/product-service.jar"]