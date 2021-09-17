FROM golang:1.12.1 AS builder
# This is taken as the base image where will base our image off of, alpine is chosen as it is a lightweight base 

RUN mkdir /app
# This makes a new directory with the name app

ADD . /app
# All of the content from the projects are copied 

WORKDIR /app
# When the image is launched as a container, this shows the current directory

RUN CGO_ENABLED=0 go build -o main ./... 
# This builds the app to the container location

FROM alpine:latest AS production
# This is the production stage of the app, as you will see it is much lighter than the build stage

COPY --from=builder /app . 
# The necessities to keep the app running are copied

CMD ["./main"]
# This the command that will run


