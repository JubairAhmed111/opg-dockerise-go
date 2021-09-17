FROM golang:1.12.0-alpine3.9
# This is taken as the base image where will base our image off of, alpine is chosen as it is a lightweight base 

RUN mkdir /app
# This makes a new directory with the name app

ADD . /app
# All of the content from the projects are copied 

WORKDIR /app
# When the image is launched as a container, this shows the current directory

RUN go build -o main . 
# This builds the app to the container location

CMD ["/app/main"]
# This the command that will run


