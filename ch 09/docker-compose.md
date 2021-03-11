**run docker-compose.yml**
**"docker-compose up" is the comand that run yml file. The default file name is "docker-compose.yml". If use other file name, should use -f as parameter**
**use -d to launch application in backend**
**"docker-compose up &" & means return to console, but log will output in console as well**
···bash
$ docker-compose up &
$ docker-compose -f another-docker-compose.yml
$ docker-compose up -d
···


**stop docker compose, service will be closed and network will be removed. But volumes will not be remove because the data is persistent in volumes**
**The images will be kept**
$ docker-compose down

**The second time run docker-compose up -d will be much more faster because no need to pull the volumes**

**check the applications status**
$ docker-compose ps

**check the process of services(containers), the PID is the process id in docker host rather than container**
$ docker-compose top

**stop and restart container**
**stop services will not delete the services**
$ docker-compose stop
$ docker-compose restart

**remove the services**
$ docker-compose rm

**if need to modify the file which host in container, check the volume**
$ docker volume inspect counter-app_counter-vol   
**then checkout the "Mountpoint", or checkout Mountpoint directly**
$ docker volume inspect counter-app_counter-vol | grep Mount

**copy the file should be changed to the mount point folder**
$ cp app.py /var/lib/docker/volumes/counter-app_counter-vol/_data/app.py

**remove all volumes**
$ docker volume prune
