FROM golang:1.24-alpine3.22

# upgrading packages
RUN apk update && \
    apk upgrade --available && \
    apk add --no-cache \
    curl

WORKDIR /app/logger
COPY ./performance-collector/performance-collector/logger/go.mod ./
COPY ./performance-collector/performance-collector/logger/go.sum ./
RUN go mod download

WORKDIR /app
COPY ./performance-collector/performance-collector/go.mod ./
COPY ./performance-collector/performance-collector/go.sum ./
RUN go mod download

# go build and exec
COPY performance-collector/performance-collector .
RUN go build -o /performance-collector
CMD [ "/performance-collector" ]
