#
# Build stage
#
FROM maven:3.6.0-jdk-11-slim AS build

# Update distribution
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y git

RUN git clone https://github.com/volfendeka/news_aggregator.git /home/app

RUN mvn -f /home/app/pom.xml clean package

#
# Package stage
#
FROM openjdk:11-jre-slim
COPY --from=build /home/app/target/aggregator-0.0.1-SNAPSHOT.jar /usr/local/lib/aggregator.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/usr/local/lib/aggregator.jar"]