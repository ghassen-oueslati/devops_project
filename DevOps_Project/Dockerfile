FROM maven:3.8.1-openjdk-11-slim AS downloader
ARG VERSION
ARG NEXUS_URL
ARG GROUP_ID
ARG ARTIFACT_ID
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:get -DremoteRepositories=${NEXUS_URL} -DgroupId=${GROUP_ID} -DartifactId=${ARTIFACT_ID} -Dversion=${VERSION} -Dtransitive=false && \
    mvn dependency:copy -Dartifact=${GROUP_ID}:${ARTIFACT_ID}:${VERSION} -DoutputDirectory=.

FROM openjdk:11-jre-slim
WORKDIR /app
COPY --from=downloader /app/${ARTIFACT_ID}-${VERSION}.jar ./app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
