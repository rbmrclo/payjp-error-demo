FROM golang:1.15-alpine
RUN apk add --no-cache git

ENV GO111MODULE on
RUN go get github.com/rbmrclo/payjp-go/v1
RUN echo "done"
