FROM golang:latest as builder

WORKDIR /go/src/github.com/JekaTka/microservices-in-golang/consignment-cli

COPY . .

RUN go get -u github.com/golang/dep/cmd/dep
RUN dep ensure -update
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .


FROM alpine:latest

RUN apk --no-cache add ca-certificates

RUN mkdir -p /app
WORKDIR /app

ADD consignment.json /app/consignment.json
COPY --from=builder /go/src/github.com/JekaTka/microservices-in-golang/consignment-cli/consignment-cli .

CMD ["./consignment-cli"]