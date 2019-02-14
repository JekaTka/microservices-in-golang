FROM golang:latest as builder

WORKDIR /go/src/github.com/JekaTka/microservices-in-golang/consignment-cli

COPY . .

RUN go get -u github.com/golang/dep/cmd/dep
RUN go get -u github.com/micro/protobuf/proto
RUN go get -u github.com/micro/protobuf/protoc-gen-go
RUN dep ensure -update
# RUN go version
# RUN ls -la
# RUN go install ./vendor/github.com/golang/protobuf/protoc-gen-go
# RUN go get -u google.golang.org/grpc
# RUN cd ~ && git clone https://github.com/golang/protobuf && cd ~/protobuf/protoc-gen-go && go install 
# RUN curl -OL https://github.com/google/protobuf/releases/download/v3.7.0rc2/protoc-3.7.0-rc-2-linux-x86_64.zip
# RUN unzip protoc-3.7.0-rc-2-linux-x86_64.zip -d protoc3
# RUN sudo mv protoc3/bin/* /usr/local/bin/
# RUN sudo mv protoc3/include/* /usr/local/include/
# RUN go get -u github.com/golang/protobuf/protoc-gen-go
# RUN export PATH=$PATH:$GOPATH/bin
# RUN echo $PATH
# RUN ls -la $GOPATH/bin 
# RUN ls -la ./vendor/github.com/golang/protobuf


# RUN go install ./vendor/github.com/golang/protobuf/protoc-gen-go/
# RUN go install ./vendor/github.com/grpc-ecosystem/grpc-gateway/protoc-gen-grpc-gateway/
# RUN protoc --version
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo .


FROM alpine:latest

RUN apk --no-cache add ca-certificates

RUN mkdir -p /app
WORKDIR /app

ADD consignment.json /app/consignment.json
COPY --from=builder /go/src/github.com/JekaTka/microservices-in-golang/consignment-cli/consignment-cli .

CMD ["./consignment-cli"]