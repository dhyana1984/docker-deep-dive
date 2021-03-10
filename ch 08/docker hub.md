**login docker hub**
$ docker login # then input the username and password 

**add tag for image**
**docker will set Registry=docker.io and Tag=latest as default value, but will not set default Repository**
**new tag will not cover current tag**
$ docker image tag web:latest(current tag) dhyana1984/web:latest(new tag)

**push to docker hub**
**the repository that image need to push is docker.io/dhyana1984/web:latest**
$ docker image push dhyana1984/web:latest

**run container. -d means run in backend, -p means mapping docker host port to container port**
$ docker container run -d --name c1 -p 80:8080 web:latest 

**check the instructions when build image**
$ docker image history web:latest

**multi-build**

# create a new storefront dev image
FROM node:latest AS storefront
WORKDIR /usr/src/atsea/app/react-app
COPY react-app .
RUN npm install
RUN npm run build

# create a new appserver dev image
FROM maven:latest AS appserver
WORKDIR /usr/src/atsea
COPY pom.xml .
RUN mvn -B -f pom.xml -s /usr/share/maven/ref/settings-docker.xml dependency:resolve
COPY . .
RUN mvn -B -s /usr/share/maven/ref/settings-docker.xml package -DskipTests

# using COPY --from to copy the production needed part from storefront and appserver
# this production image is much more smaller than the image with dev tools
FROM java:8-jdk-alpine AS production
RUN adduser -Dh /home/gordon gordon
WORKDIR /static
COPY --from=storefront /usr/src/atsea/app/react-app/build/ .
WORKDIR /app
COPY --from=appserver /usr/src/atsea/target/AtSea-0.0.1-SNAPSHOT.jar .
ENTRYPOINT ["java", "-jar", "/app/AtSea-0.0.1-SNAPSHOT.jar"]
CMD ["--spring.profiles.active=postgres"]
