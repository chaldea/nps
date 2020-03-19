FROM golang:alpine AS build
ENV GO111MODULE=on
ENV GOPROXY=https://goproxy.io
WORKDIR /src
COPY . .
RUN go build cmd/nps/nps.go

FROM alpine:latest AS run
WORKDIR /nps
COPY --from=build /src/web/static ./web/static
COPY --from=build /src/web/views ./web/views
COPY --from=build /src/conf ./conf
COPY --from=build /src/certs ./certs
COPY --from=build /src/nps ./nps
RUN mkdir -p data
VOLUME ["/nps/conf","/nps/certs","/nps/data"]
ENTRYPOINT [ "./nps" ]