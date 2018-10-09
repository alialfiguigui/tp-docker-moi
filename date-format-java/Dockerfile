FROM maven:3-jdk-8-alpine as builder

WORKDIR /usr/src/app

COPY pom.xml ./

# Ligne optionnelle (sous-entendue par "mvn package")
# mais qui permet de tirer profit de la mise en cache
RUN mvn dependency:go-offline

COPY src src/
RUN mvn package -B

FROM openjdk:8-jre-alpine
WORKDIR /usr/src
COPY --from=builder /usr/src/app/target/date-format-java-*.jar app.jar

# Voir https://discuss.pivotal.io/hc/en-us/articles/230141007
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar", \
  "/usr/src/app.jar"]

# docker build -t date-format-java .
# docker run --rm -it date-format-java #..
