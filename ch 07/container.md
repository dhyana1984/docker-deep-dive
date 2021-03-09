# --restart always will always try to restart the container which is stop if not use "docker container stop" to stop the container
# the container will restart when Docker Deamon is restart if using --restart always
$ docker container run --name neversaydie -it --restart always alpine sh

# the container will not restart when Docker Deamon is restart if using --restart unless-stopped
$ docker container run --name neversaydie -it --restart unless-stopped alpine sh

# the container will restart if exit container and return value is not 0
# the container will restart when Docker Deamon is restart if using --restart on-failure
$ docker container run --name neversaydie -it --restart on-failure alpine sh


# -d means run in the backend, current console will not connect to container
# -p means make Docker host's port mapping to container. In this case, -p 80:8080 means mapping Docker's 80 port to container's 8080 port
$ docker container run -d --name webserver -p 80:8080 nigelpoulton/pluralsight-docker-ci

# make the application launch cmd in the image
# see the "Cmd" secion of inspect result
$ docker image inspect  nigelpoulton/pluralsight-docker-ci
 "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"/bin/sh\" \"-c\" \"cd /src && node ./app.js\"]"
            ]

# delete all the containers
$  docker container rm $(docker container ls -aq) -f 