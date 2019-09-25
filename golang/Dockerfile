FROM golang:1.13.0-alpine3.10 as basic

RUN mkdir -p /go/src/app
WORKDIR /go/src/app
COPY . .

RUN apk update && apk upgrade && apk add --no-cache bash git openssh
RUN go mod download
RUN go build .

FROM alpine:latest as prod
WORKDIR /root/
COPY --from=basic /go/src/app/buse .

EXPOSE 8000
ENTRYPOINT ["./buse"]