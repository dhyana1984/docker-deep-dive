# the first line is always "FROM", define the image as a basic image layer
# the rest of image layer will be added on this
FROM alpine

# "LABEL" is a key-value pair. This is a image metadata
LABEL maintainer="xiongyi_1984@foxmail.com"

# "RUN" will create a new image layer on the basic image layer
# Install Node and NPM
RUN apk add --update nodejs nodejs-npm

# "CPOY" will create a new image layer as well
# Copy app to /src
COPY . /src

# Meta data, set work directory
WORKDIR /src

# Create a new image layer
# Install dependencies
RUN  npm install

# Metadata
EXPOSE 8080

# Metadata, set the entry application of image
ENTRYPOINT ["node", "./app.js"]
