### How to create our own image using Dockerfiles ?
- Create 1 repo in github for this Dockerfile.
- Create 1 folder "FROM" this is nothing but first instruction because we need base OS, you can refer in
  docker references website.
- Then write Dockerfile inside the FROM folder.
- File should be "Dockerfile" D must be capital letter. Go through the code in VS.
- Create 1 instance for docker and login, install docker init.
- Clone the git repo in the docker server, and go to the FROM folder
- Now build docker image here using "docker build -t <URL>/<USERNAME>/IMAGE:VERSION ."
