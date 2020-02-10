FROM golang:latest as build

RUN mkdir -p ~/go/src/service
WORKDIR ~/go/src/service

RUN go get -d go.opencensus.io/... && \
	go get -d contrib.go.opencensus.io/exporter/prometheus

COPY cmd/main.go . 

RUN CGO_ENABLED=0 go build -a -installsuffix cgo --ldflags "-s -w" -o /usr/bin/server 

FROM alpine:3.7

COPY --from=build /usr/bin/server /root/

EXPOSE 8010
WORKDIR /root/

CMD ["./server"]