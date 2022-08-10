
# This is a demo project. How should a Golang project build a image
# 这是一个演示项目，来说明一个golang项目应该如何构建镜像

FROM golang:1.17.5-alpine3.15 AS build

WORKDIR /home/work
COPY . .

# build your project
RUN export GO111MODULE=on && export GOPROXY="https://goproxy.cn,direct"
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -ldflags "-X main.version=`cat VERSION`"


# run your project
FROM alpine:3.15 AS run
RUN apk update && apk add --no-cache ca-certificates
COPY --from=build /home/work/yourbin /home/bin

EXPOSE 8080

WORKDIR /home/bin
ENTRYPOINT ["./yourbin"]