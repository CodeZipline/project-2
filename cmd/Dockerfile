#build stage
FROM golang:alpine AS builder 
ARG B_ORIGIN_PORT="8081"
RUN echo "ARGS is ${B_ORIGIN_PORT}"
RUN mkdir /app 
ADD . /app
WORKDIR /app
RUN apk add build-base
#The --no-cache option allows to not cache the index locally, which is useful for keeping containers small.
#Literally it equals apk update in the beginning and rm -rf /var/cache/apk/* in the end.
RUN apk add --no-cache git && apk update
#Obtain all the dependency to run the functions
RUN go get -d
RUN go build -o main ./main.go

#execute stage
FROM alpine:latest AS production
COPY --from=builder /app .
EXPOSE 8081
CMD [ "./main" ]
#docker build [arg]