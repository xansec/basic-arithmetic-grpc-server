FROM golang

WORKDIR /work
COPY . .
RUN go mod tidy
RUN go get \
  github.com/bufbuild/buf/cmd/buf \
  github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway \
  github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2 \
  google.golang.org/grpc/cmd/protoc-gen-go-grpc \
  google.golang.org/protobuf/cmd/protoc-gen-go
RUN go install \
  github.com/bufbuild/buf/cmd/buf \
  github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-grpc-gateway \
  github.com/grpc-ecosystem/grpc-gateway/v2/protoc-gen-openapiv2 \
  google.golang.org/grpc/cmd/protoc-gen-go-grpc \
  google.golang.org/protobuf/cmd/protoc-gen-go
RUN buf generate --path ./proto/arithmetic/arithmetic.proto

EXPOSE 8090
ENV GRPC_TRACE=all
ENV GRPC_VERBOSITY=debug
CMD ["go", "run", "main.go"]
