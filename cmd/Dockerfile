#build stage
FROM golang:alpine AS builder 
RUN mkdir /app 
ADD . /app
WORKDIR /app
#The --no-cache option allows to not cache the index locally, which is useful for keeping containers small.
#Literally it equals apk update in the beginning and rm -rf /var/cache/apk/* in the end.
RUN apk add --no-cache git
#Obtain all the dependency to run the functions
RUN go get -d
RUN go build -o main ./main.go

#execute stage
FROM alpine:latest AS production
COPY --from=builder /app .
EXPOSE 8081
CMD [ "./main" ]