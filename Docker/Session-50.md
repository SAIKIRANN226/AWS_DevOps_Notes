### RUN instruction in Dockerfiles
The RUN instruction in a Dockerfile executes commands during the image build process. Each RUN instruction creates a new layer in the Docker image, capturing the changes made by the executed command. Go to the RUN folder in server and "docker build -t run:v1 ."

### RUN vs CMD instruction ?
When you do "systemctl start catalogue" it will create 1 nodejs process and this process will run for infinite times, until this process is running, then only we can say catalogue application is running, if this process is stopped, then your application is not running. Here CMD instruction is to make your container running ; RUN instruction will run at the time of image building ; CMD instruction will run at the time of container creation. As we know container is the running version of image, if container is running that means there is something that keeps it running, that is nothing but CMD instruction, so to make container to run infinite times, we use CMD instruction. What should we keep in CMD to run container continuously ? Then use the command
"docker build -t cmd:v1"




### Points to remember
- Systemctl commands will not work in containers, to work it should be main OS, but container is not using
  main OS right ? it is only using base OS. We need to give command manually.
