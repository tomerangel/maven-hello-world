# the first stage of our build will use a maven 3.6.1 parent image
FROM maven:3.6.1-jdk-8-alpine AS MAVEN_BUILD
WORKDIR usr/app
# copy the pom and src code to the container
COPY ./ ./
# package our application code
# RUN mvn clean package
# the second stage of our build will use open jdk 8 on alpine 3.9
RUN cd target && ls
RUN pwd
FROM openjdk:8-jre-alpine3.9
ENV SERVICE_NAME="tomer"

RUN addgroup --gid 1001 -S $SERVICE_NAME && \
    adduser -G $SERVICE_NAME --shell /bin/false --disabled-password -H --uid 1001 $SERVICE_NAME && \
    mkdir -p /var/log/$SERVICE_NAME && \
    chown $SERVICE_NAME:$SERVICE_NAME /var/log/$SERVICE_NAME
# copy only the artifacts we need from the first stage and discard the rest
COPY --from=MAVEN_BUILD /usr/app/target/my-app-1.0.1.jar /my-app.jar
# set the startup command to execute the jar
USER $SERVICE_NAME
CMD ["java", "-jar", "/my-app.jar"]
