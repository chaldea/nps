FROM golang:alpine AS build
ENV GO111MODULE=on
ENV GOPROXY=https://goproxy.io
WORKDIR /src
COPY . .
RUN go build cmd/npc/npc.go

FROM alpine:latest AS run
WORKDIR /npc
COPY --from=build /src/npc ./npc
ENV SERVER_ADDR=127.0.0.1:8024
ENV CONN_TYPE=tcp
ENV VKEY=1234
ENTRYPOINT [ "sh", "-c", "./npc -server=${SERVER_ADDR} -vkey=${VKEY} -type=${CONN_TYPE}" ]