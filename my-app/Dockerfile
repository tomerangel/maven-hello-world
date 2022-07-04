# the first stage of our build will use a maven 3.6.1 parent image
FROM maven:3.6.1-jdk-8-alpine AS MAVEN_BUILD
WORKDIR usr/app
# copy the pom and src code to the container
COPY ./ ./
# package our application code
# RUN mvn clean package - if we want to do build right here! without doing it on steps CI so we dont need to copy all only pom.xml
# the second stage of our build will use open jdk 8 on alpine 3.9
FROM openjdk:8-jre-alpine3.9
# ii.	The  Docker image shouldn't run with root 
ENV SERVICE_NAME="tomer"
RUN addgroup --gid 1001 -S $SERVICE_NAME && \
    adduser -G $SERVICE_NAME --shell /bin/false --disabled-password -H --uid 1001 $SERVICE_NAME && \
    mkdir -p /var/log/$SERVICE_NAME && \
    chown $SERVICE_NAME:$SERVICE_NAME /var/log/$SERVICE_NAME
# copy only the artifacts we need from the first stage and discard the rest
# COPY /home/runner/work/maven-hello-world/maven-hello-world/target/my-app-1.0.1.jar /app/my-app.jar -- copy from artifact!! but the bouns we want multistage docker!
COPY --from=MAVEN_BUILD /usr/app/target/my-app-1.0.1.jar /my-app.jar
# set the startup command to execute the jar
EXPOSE 8080
USER $SERVICE_NAME
CMD ["java", "-jar", "/my-app.jar"]

# Bonus – do as much as possible from the above using Multistage Docker 
