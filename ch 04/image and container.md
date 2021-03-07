# pull image
$ docker image pull ubuntu:latest

# check the images
$ docker images
$ docker image ls

# check the containers
$ docker container ls -a

# run container
# -t check current consle to container
# /bin/bash run bash 
$ docker container run -it ubuntu:latest /bin/bash

# press ctrl+pq to quit container console

# connect to container
# c230c515bd17 is the id of container
$ docker container exec -it c230c515bd17 bash

# stop container
$ docker container stop c230c515bd17

# remove container
$ docker container rm c230c515bd17

# remove image
$ docker image rm c230c515bd17

# build image from docker file
# run this command in the docker file
# please note that all the source file should be in the same folder because the build command will copy them in to image
$ docker image build -t test:latest .