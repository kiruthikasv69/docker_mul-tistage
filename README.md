This Dockerfile has 5 layers in total:

Base image (FROM ubuntu)

Installing dependencies (RUN apt-get install)

Setting environment variable (ENV)

Copying source files (COPY . .)

Building the application (RUN go build)
