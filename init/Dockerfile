FROM golang:1.8-alpine as builder

WORKDIR $GOPATH/src/github.com/Boostport/kubernetes-vault

COPY . .

RUN apk --update add gcc git musl-dev \
 && go get -u github.com/Masterminds/glide \
 && glide install --strip-vendor \
 && cd init \
 && go build -o kubernetes-vault-init

FROM alpine:3.5
LABEL maintainer Francis Chuang <francis.chuang@boostport.com>

COPY --from=builder /go/src/github.com/Boostport/kubernetes-vault/init/kubernetes-vault-init /kubernetes-vault-init

ENTRYPOINT ["/kubernetes-vault-init"]