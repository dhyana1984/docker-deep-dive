# pull image
# lastest tag is not a mandtory tag, it cannot make sure point to the newest version
$ docker image pull ubuntu:latest #118MB
$ docker image pull alpine:latest #4MB
$ docker image pull microsoft/powershell:nanoserver #1.21GB
$ docker image pull microsoft/dotnet:latest #1.65GB

# filter image
# dangling is the image that is without tag
# --filter danling = true/false
# --filter before = imageId #return the images created before
# --filter since = imageId  #return the images created after
# --filter label = xxx  #filter by label
# --filter reference = "*:latest" 
$ docker image ls --filter dangling=true
$ docker image ls --filter=reference="*:latest"

# remove all dangling image
$ docker image prune

# remove all dangling image and no container image
$ docker image prune -a

# search Docker Hub via CLI
# --filter "is-official=true" to filter the oficial image
# docker search only returns 25 lines, but user can add --limit to increase the rows of result. The max row is 100
$ docker search <name>

# check the layer and metadata of image
$ docker image inspect ubuntu:latest

# check the digest of image
$ docker image ls -a --digests alpine

# pull image via digest
$ docker image pull alpine@sha256:a75afd8b57e7f34e4dad8d65e2c7ba2e1975c795ce1ee22fa34f8cf46f96a3be

# delete all the images
# docker image ls -q only return the image's ID
# $(docker image ls -q) means pass the images' ID to docker image rm
$ docker image rm $(docker image ls -q) -f 
