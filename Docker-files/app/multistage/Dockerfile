FROM maven:3.9.9-eclipse-temurin-17-jammy AS build_image
RUN git clone https://github.com/hkhcoder/vprofile-project.git
WORKDIR /vprofile-project
RUN git checkout docker

ENV MAVEN_OPTS="-Xms256m -Xmx1024m"
RUN mvn clean package -DskipTests

FROM tomcat:10-jdk17
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=build_image /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
