VERSION 0.6
FROM golang:1.19-alpine
WORKDIR /build

deps:
    COPY go.mod go.sum ./
    RUN go mod download && go mod verify

build:
    FROM +deps
    COPY pkg pkg
    COPY *.go .
    COPY *.libsonnet .
    RUN go build -o dist/docsonnet .
    SAVE ARTIFACT dist/docsonnet /docsonnet

image:
    FROM alpine:3.12
    COPY +build/docsonnet /usr/bin/docsonnet
    ENTRYPOINT "/usr/bin/docsonnet"
    SAVE IMAGE --push docker.io/technofab/docsonnet
