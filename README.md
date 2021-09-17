# Technical challenge

This repository forms the basis of our technical challenge and is used with in our hiring process.

Our production environments utilise AWS cloud platform with the infrastructure being created and controlled by Hashicorp's Terraform. Our deployment process takes the app code repository, generates a series of docker images which are then placed into AWS Elastic Cluster Service.

# Application

This repository contains a Go application (inside the ./app folder) that acts as an API; it is configured to respond on port 8080 and has two endpoints (/ and /status) that return json content.

The /status endpoint returns different content and http response code depending on the value of an environment variable called APP_STATUS. When APP_STATUS=OK the /status endpoint will return a 200 code and message, otherwise it will return a 500 code.

You can run the application directly using go run ./app/main.go from the root of this repository.

# The challenge

We would like you to create a fork of this repository which expands on the existing code. Aim to provide a working docker image based on the included application where both endpoints of the API return a 200 http status code.

Please include an updated README.md with steps to run your solution along with notes to document your approach and process.

Complete the task at your own pace, we recommend around an hour and a half of focus, this can be spread out and is not a strict factor.

Do not worry if you are not able to fully complete the task, we are more interested in your approach then a perfect solution.

To help guide you in this task, we've outlined some typical steps (in no particular order) that would be needed.

# Creating a Dockerfile

- Building the Go app
- Mapping ports
- Setting up Docker on your local machine
- Passing environment variables

# Getting started

While I had previous experience of Docker, it was mainly following tutorials so this was my first ever real life Docker project, I learnt a lot more by learning from the mistakes I made during this project.
Golang is a langauge app that I never heard of before this project, so after the initial panic, I looked at this as a learning curve to improve my problem solving skills. These are the questions I wrote down so I could answer them: 
 - `What is Golang?`
 - `What can help me learn it?`
 - `Who can help me learn it?` 

These questions were answered very quickly by one person, my mentor Sam Joseph, a software developer at the MoJD&T. He recommended the book, Tour of Go, which I combined with tutorials off YouTube to learn the fundamentals of Golang and to actually understand the task.

After learning the fundamentals of Golang, I returned to focus on the task, I refreshed myself on how to use Docker, making sure that I had the latest version of both Golang and Docker installed.

# Creating the Dockerfile and DockerCompose
Now it was time to create the Dockerfile, but first I followed the instructions to check if the http response code returned a 200 message when I ran go run main.go in the VSCode terminal. NOTE: I made sure I downloaded the Go extensions on VSCode to ensure everything ran smoothly. After the commands were inputted into the Dockerfile and the DockerCompose.yaml file, I returned to the VSCode terminal to build the Docker image using:

 `docker build -t moj-app . `

An error was made at this point as I forgot to and the ` . ` at the end. The ` -t `represents a tag. It took a few minutes to build the image. To see if the image was built, I ran:

`docker images`

This shows the image along with it's image number, name, and when it was created. I then ran the Docker image using:

`docker run -d -p 8080:8080 moj-app`

The ` -d ` allows the container to run in detached mode, and the ` -p `sets the port number to `8080`.

To check if the container is now running at port `8080`, I typed in `localhost:8080` in my web browser, and SUCCESS! Days of learning came into fruition and it was running.

I then closed and removed the containers using:

`docker container stop <container_id>`

Then

`docker rm <container_id>`

To check if it's been removed, there should be no indication of the container when the following is inputted:

`docker ps`

To remove the image and check if it has beend deleted:

`docker stop <container_id>`

Then

`docker rm <container_id>`

To check if it has been removed:

`docker ps`

# Creating a Multi-stage Dockerfile

Due to the large size of the image created in the steps before, a multi-stage Dockerfile is used to create two stages, a build and production stage. The build stage carries most of the memory, while the production stage is uploaded to the repository to be distributed. As seen by the updated Dockerfile, there are now two stages being built but the code to build and run the docker image is the same:

`docker build -t moj-multistage-app .`

`docker run -d -p 8080:8080 moj-multistage-app`

# Next steps

There are two features that I want to implement to further my learning:

- `CI/CD` - Using GitHub actions to automate monotonous tasks and to remove errors. CI/CD was recently implemented in MOJ D&T and has reduced the update wait time from 2 weeks to immediate access.
- `Kubernetes` - Containerising the Golang app and deploying into a kubernetes cluster to improve scalability of the app when there are many users involved.

# What went well

This whole learning process made me realise how important it is to reach out to senior members of the team when I am struggling. Just a simple tip can help understand the project, so thank you for giving me this opportunity to build on my skills and implement them on a real life project.

# Even better if

I would ask someone to pair programme with as it is easier for us to understand and learn from mistakes, showing agile methodology. It is also very good, as the foundations of the language I am learning become stronger when I explain it to a partner.

Thank you for taking the time out to read my README :)
